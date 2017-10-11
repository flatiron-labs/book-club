# Testing Channels and OTP

```
defmodule TestBackend do
  def start_link(query, ref, owner, limit) do
    Task.start_link(__MODULE__, :fetch, [query, ref, owner, limit])
  end

  def fetch("result", ref, owner, _limit) do
    send(owner, {:results, ref, [%Result{backend: "test", text: "result"}]})
  end
  def fetch("none", ref, owner, _limit) do
    send(owner, {:results, ref, []})
  end

	test "compute/2 with backend results" do
    assert [%Result{backend: "test", text: "result"}] = InfoSys.compute("result", backends: [TestBackend])
  end

  test "compute/2 with no backend results" do
    assert [] = InfoSys.compute("none", backends: [TestBackend])
  end
end
```

## Testing InfoSys

- Build a stub for our backends and pass into application code using dependency injection
- cheating is ok, we’re testing how `InfoSys` responds to stubbed  behavior from a backend
- For testing process failures/timeouts, *do not* use `Process.alive?(pid)`, instead use `Process.monitor` to monitor the process and then catch the process failing in the `DOWN` handler
- Interesting how the use a standard interface for `Backend` to easily create a stub backend
- Since messages are async, important to know that `assert_receive` waits for 100 ms by default before failing the test (can pass in arg as well)
- `refute_received` vs `refute_receive`: `received` doesn’t wait 100ms, instead checks message inbox immediately (faster test)
- `@tag :capture_log` to suppress log messages unless it’s a failing test


## Testing Wolfram

- Elixir community emphasizes not mocking
- Mocking libraries usually change global  behavior by replacing functions on a module with the mock
	- Test cannot be run concurrently if this is the case
	- (mocking http to remove the API call)
- Mocking deps can snowball, obscuring the functionality they’re meant to test
- Identify hard to test live code and build a configurable, replacable testing implementation.
- Then make the code pluggable in your module so you can swap out in different environments
	- (could we apply to docker platform adapter for testing interactions to Docker)

```
@http Application.get_env(:info_sys, :wolfram)[:http_client] || :httpc defp fetch_xml(query_str) do
  {:ok, {_, _, body}} = @http.request( String.to_char_list("http://api.wolframalpha.com/v2/query" <> "?appid=#{app_id()}" <> "&input=#{URI.encode_www_form(query_str)}&format=plaintext")) body
end
```

- Stub the external client / module
- no longer testing wolfram alpha, but instead how our code handles and parses the response provided
- `Code.require_file "backends/http_client.exs", __DIR__`to require test modules in the `test_helper.exs`

```
defmodule InfoSys.Backends.WolframTest do
  use ExUnit.Case, async: true
  alias InfoSys.Wolfram

  test "makes request, reports results, then terminates" do
    ref = make_ref()
    {:ok, _} = Wolfram.start_link("1 + 1", ref, self(), 1)
    assert_receive {:results, ^ref, [%InfoSys.Result{text: "2"}]}
    end
  end
```
- Test the `Result` struct response based on WA results

- Test process terminates (again with `Process.monitor`):

```
test "makes request, reports results, then terminates" do
  ref = make_ref()
  {:ok, pid} = Wolfram.start_link("1 + 1", ref, self(), 1)
  Process.monitor(pid)
  assert_receive {:results, ^ref, [%InfoSys.Result{text: "2"}]}
  assert_receive {:DOWN, _ref, :process, ^pid, :normal}
end
```


- Multiple layers of the stack you can start stubbing behavior out like this and causing global changes and complicated mocking strategies
	- In these cases, [Bypass](https://github.com/PSPDFKit-labs/bypass) can provide a mocked HTTP server for your requests

## Testing Channels
- Channels are OTP servers under the hood
- Phoenix includes the `Phoenix.ChannelTest` module 
	- provides testing assertions for pushing messages to client, replies to messages, and broadcasts

### Testing the Socket
- Authenticate a user to the socket by creating a valid one with `Phoenix.Token.sign!`


### Channel
- use `setup do … end` to set up your test (return {:ok, state} tuple  to pass to the tests (GenServer under the hood?)
- `subscibe_and_join` to simulate client joining a channel
- can test changes in `socket.assigns` state as well as the `reply` returned from the join
- can test using `push` and `assert_reply` on the active channel & `assert_broadcast` to test broadcast responses to incoming messages from the WS



Really loving the message passing pattern and limiting state and trying to keep everything pure functions.
Fixes one of the things I don’t like about OO programming. So much state that can snowball out of control, requiring:
	- Statefulness accumulating other state fulness
	- objects that can’t interact with other objects effectively because their behavior is too unpredictable and complicated depending on their state
	- Now testing behavior becomes way simpler because behavior is completely separate from data. OO encourages behavior to change based on internal state of the object. Functional programming encourages data to be dependency injected into the behavior, allowing much easier testing and easier to reason about code


EASY AND SIMPLE RIGHT?!?!?!?!!?
