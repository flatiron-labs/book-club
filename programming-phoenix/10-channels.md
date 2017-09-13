# Ch. 10 Channels
- HTTP stateless model doesn’t work for highly interactive app
- The request - response cycle has too much overhead
- client connects to a channel and then just sends and receives messages

## Channels
- conversation: sends & receives messages, keeps state
- messages called `events`
- state is kept on the channel in a struct called `socket`
- channels commonly map to:
	- chat room
	- local map
	- game
	- video annotations
	- any kind of shared topic where more than one user might be interested
- powerful because *every channel has its own isolated, dedicated process*
- state becomes easier to track…no more needing to use cookies or database
	- one crashing process won’t affect other users
- 3 things:
	- making and breaking connections
	- sending messages
	- receiving messages

```
import Player from "./player"

let Video = {

  init(socket, element){ if(!element){ return }
    let playerId = element.getAttribute("data-player-id")
    let videoId  = element.getAttribute("data-id")
    socket.connect()
    Player.init(element.id, playerId, () => { 
      this.onReady(videoId, socket)
    })
  },

  onReady(videoId, socket){
    let msgContainer = document.getElementById("msg-container")
    let msgInput     = document.getElementById("msg-input")
    let postButton   = document.getElementById("msg-submit")
    let vidChannel   = socket.channel("videos:" + videoId)
    // TODO join the vidChannel
  }
}
export default Video
```

## UserSocket
- Entry point for socket connections, responsible for wiring up the socket with channels.
- Authenticate the user to determine which channels to join
- Provides a `socket` abstraction decoupled from any underlying transport protocol. Can use websockets, long polling, future protocols, etc

## Channels
- Topics that are generally named `topic:subtopic`
- define channel topics to join through pattern matching:
```
defmodule Rumbl.UserSocket do use Phoenix.Socket
## Channels
channel "videos:*", Rumbl.VideoChannel
```

## Channel Modules
- define channel modules that provide callbacks for managing a channel’s events and lifecycle
- `join`: when a socket joins the channel
- return `{:ok, socket }` to authorize the channel join
- return `{:error, socket}` to deny the channel join

```
  onReady(videoId, socket){
    let msgContainer = document.getElementById("msg-container")
    let msgInput     = document.getElementById("msg-input")
    let postButton   = document.getElementById("msg-submit")
    let vidChannel   = socket.channel("videos:" + videoId) 

    vidChannel.join()
      .receive("ok", resp => console.log("joined the video channel", resp) )
      .receive("error", reason => console.log("join failed", reason) ) 
```


```
def join("videos:" <> video_id, _params, socket) do
	:timer.send_interval(5_000, :ping)
	{:ok, socket}
end

def handle_info(:ping, socket) do
	count = socket.assigns[:count] || 1
	push socket, "ping", %{count: count}
	{:noreply, assign(socket, :count, count + 1)}
end
```

- `handle_info`: reply to elixir processes (`ping` example)
- `noreply`: no reply back to the elixir process, (however `push` is sending down the message)

```
import Player from "./player"

let Video = {

  init(socket, element){ if(!element){ return }
    let playerId = element.getAttribute("data-player-id")
    let videoId  = element.getAttribute("data-id")
    socket.connect()
    Player.init(element.id, playerId, () => {
      this.onReady(videoId, socket)
    })
  },

  onReady(videoId, socket){
    let msgContainer = document.getElementById("msg-container")
    let msgInput     = document.getElementById("msg-input")
    let postButton   = document.getElementById("msg-submit")
    let vidChannel   = socket.channel("videos:" + videoId)

    postButton.addEventListener("click", e => {
      let payload = {body: msgInput.value, at: Player.getCurrentTime()}
      vidChannel.push("new_annotation", payload)        
                .receive("error", e => console.log(e) ) 
      msgInput.value = ""
    })

    vidChannel.on("new_annotation", (resp) => {         
      this.renderAnnotation(msgContainer, resp)
    })

    vidChannel.join()
      .receive("ok", resp => console.log("joined the video channel", resp) )
      .receive("error", reason => console.log("join failed", reason) )
  },

  renderAnnotation(msgContainer, {user, body, at}){
    // TODO append annotation to msgContainer
  }
}
export default Video
```

### Socket can behave synchornously
- allows flexibility of using request - response cycle
```
vidChannel.push("new_annotation", payload)
			.receive("error", e => console.log(e) )
```


### Broadcast changes in socket state
```
def handle_in("new_annotation", params, socket) do
	broadcast! socket, "new_annotation", %{
		user: %{username: "anon"},
		body: params["body"],
		at: params["at"]
	}
	{:reply, :ok, socket}
end
```
#bookclub


## Authentication
- token based authentication preferred over session based
- accessing cookies in Websockets is insecure
- auth plug already authenticates
- will then generate a token sent down to the client
- client sends token when creating the socket

## Connecting to Channels
genrating token:
```
token = Phoenix.Token.sign(conn, "user socket", user.id)
conn
|> assign(:current_user, user) |> assign(:user_token, token)
```

verifying:
```
@max_age 2 * 7 * 24 * 60 * 60
def connect(%{"token" => token}, socket) do
	case Phoenix.Token.verify(socket, "user socket", token, max_age: @max_age) do
		{:ok, user_id} ->
			{:ok, assign(socket, :user_id, user_id)}
		{:error, _reason} -> :error
	end
end

def connect(_params, _socket), do: :error

def id(socket), do: "users_socket:#{socket.assigns.user_id}"
```

#### sending data on channel join (use three tuple response)
```
def join("videos:" <> video_id, _params, socket) do
	video_id = String.to_integer(video_id)
	video = Repo.get!(Rumbl.Video, video_id)
	annotations = Repo.all(
		from a in assoc(video, :annotations),
		order_by: [asc: a.at, asc: a.id], limit: 200,
		preload: [:user]
	)
	resp = %{annotations: Phoenix.View.render_many(annotations, AnnotationView, "annotation.json")}
	{:ok, resp, assign(socket, :video_id, video_id)} end
```

### Using Views for JSON serialization
```
defmodule Rumbl.AnnotationView do
	use Rumbl.Web, :view

	def render("annotation.json", %{annotation: ann}) do
	%{
		id: ann.id,
		body: ann.body,
		at: ann.at,
		user: render_one(ann.user, Rumbl.UserView, "user.json")
	}
	end
end
```


## Handling Disconnects
- data can get out of sync
- clients can disconnect, reconnect and receive duplicate data
- use `last_seen_id` on the client to send the last annotation id we know to the server so it only responds with new ones
	- Can we apply to IDE disconnects?
- `channel.params` can hold params to send when calling `join`


## Wrapping Up
- You learned to connect to a server-side channel through an ES6 client.
- We built a server-side channel with both long-polling and WebSocket support.
- We built a simple API to let users join a channel.
- We processed inbound messages from OTP with handle_info and channels
with handle_in.
- We sent broadcast messages with broadcast!.
- We authenticated users with Phoenix.Token.
- We persisted annotations with Ecto.V
