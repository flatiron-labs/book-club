# Chapter 4 - Images! How do they work? Where do they live? How are they made? Let's find out!

Commands cheat sheet:

| Command | Explanation |
|---|---|
| `docker images` | lists all images |
| `docker pull {repository}[:{image_name}]` | pulls down latest images from DockerHub repo. Can optionally request a specific image by tag. |
| `docker push` | Pushes image to dockerhub |
| `docker run` | Can combine `pull`, `build`, and `exec` if needed |
| `docker search {search_term}` | Searches DockerHub for images |
| `docker port {container_identifier} {internal_port}` | Returns what external port is mapped to a specific internal port. |
| Building Images | --- |
| `docker commit [-m {message}] {id_of_container} {username/repo_name}[:{tag}]` | Builds an images. *Not recommended* |
| `docker build [-t="{tag_name}"] .` | Builds image from associated Dockerfile |
| `docker history {image_id}` | Shows all the build steps for the image |
| `docker rmi {image}` | Deletes and image. Can only perform if no containers with this image |

## Images, how do they work?

- A Docker image is made up of filesystems layered over each other
  - `bootfs` as the base (typical linux boot filesystem)
  - `rootfs` next which can be one or more FS
  - Each file system is an image

- Different from normal OS because root fs in Docker stays read-only.

- Docker uses 'union mount' to mount multiple file systems on top of each other.

- Each file system below is the 'parent image' until you get to the bottom, the base image.

- QUESTION: On pg 73, why is the Kernal in the `bootfs` image? I thought Docker was supposed to use the host Kernal (unless we're running on a non-linux OS).

- "Copy on write" - Modifying a file copies it up to the top level writable container but does not modify the parent image below.

## Images, where do they live?

- Images locally live in `/var/lib/docker`

- Images can live in repositories, and repos are on registries (e.g. DockerHub - like github).
  - User repos - created by felow users. To specify a user repo, you need to do `username/reponame`. e.g. -> `flatironschool/ide_docker_v4`
  - Top level repos - Created by the Docker team. To specify a top level repo, you only need the repo name. e.g. -> `ubuntu`

## Images, how are they built?

>Note: Generally create images off of existing images

### Building with commmit

- Not recommended
- Seems to allow the ability to 'take a snap shot' of current state, but generally seems more unstable
- QUESTION: When would this be good to use? Bad?

### Building with a Dockerfile

Dockerfile commands cheat sheet:

| Command | Explenation |
|---|---|
| `FROM {image}` | Starting image. Should be first line. |
| `RUN {bash_command}` | Runs specified command in container. |
| `EXPOSE {port}` | Exposes a port |
| `CMD [command, [arg1, arg2, ...]]` | Default command to be run at container launch. Can be overridden |
| `ENTRYPOINT [command, [arg1, arg2, ...]]` | Like `CMD`, but not easily overridden. By dafault, the 'override' command is passed as an arg to the entrypoint. Provides a more stable use of a container? |
| `WORKDIR {file/path}` | Sets directory to run commands |
| `ENV {VAR_NAME} {var_value}` | Sets environment variables |
| `USER {username}` | Specify what user to run commands as |
| `VOLUME ["path/to/dir"]` | Add directories to be accessible in the container, but not written to image |
| `ADD {path/on/local} {location/in/image}` | Adds files from the build dir into the image. Note: auto unpacks archive files (`gzip`, `tar`, `zip`, ...) |
| `COPY {path/on/local} {location/in/image}` | Like `ADD` but does not unpack archived files |
| `LABEL {key}={"value"}` | Adds meta data to image. Returns when `docker inspect {image}` is called |
| `STOPSIGNAL` | Sets system call for when container is stopped? |
| `ARG {key}[={value}]` | Sets args to be passed at build. Can specify default |
| `SHELL` | Can specify shell that commands are run in. Bash? ZSH? Powershell? |
| `HEALTHCHECK {criteria}` | Sets criteria for what a healthy container looks like |
| `ONBUILD {use another command here}` | Specifies a command to be run on build of image |

full list: https://docs.docker.com/engine/reference/builder/

- A Dockerfile  files in a directory and contains instructions on how to build an image
- The directory that it is in is called a context / build context. Docker deamon will have access to these files _when building_

- Docker runs the base image, then executes a command from the Dockerfile, then commits it, then runs that image... and repeats the process
  - Each line of the docker file builds a new image with it's own unique ID
  - **PRO TIP: When a line fails, you can `docker run -it {image_id} /bin/bash` to hop in and manually try the command that failed for debugging.**

- Dockerfile's context does not have to be the dir it is in. Can also specify another dir or even a github dir with something like `docker build github.com/flatiron-labs/ironboard`

- A `.dockerignore` file in context allows certain files and directories to be excluded from the build just like `.gitignore`

- Since Docker caches each layer of a Dockerfile, it's helpful to put commands that may change frequently near the bottom for faster builds in the future. If you decide you don't want caching, this can be done with `--no-cache` flag.
  - Pros:
    - Quicker builds off previous images
  - Cons:
    - Using previous templates may mean using out of date packages

- When running a container, you can specify port mapping with `docker run -p {external_port}:{internal_port}`
  - `internal_port` being the port as seen from inside of the container
  - `external_port` being the port as seen from the host
  - `-P` can also be used to publish all `EXPOSE`d ports on random ports for the local host

Automated Builds
- Can connect a code repo got autobuilding (creating an image when code is updated)

Don't like DockerHub? Run your own registry from a container with: `docker run -d -p 5000:5000 --name registry registry:2`

Push to a custom registry by tagging the image with `registry_url/username/image_name` and then calling `docker push` on it. 

QUESTION: Why use `WORKDIR` as opposed to `cd`?
QUESTION: With `VOLUME`, how do you specify external and internal locations?
QUESTION: Does using `ONBUILD` ensure that no following layers can be cached because `ONBUILD` layers must be re-run any time there is a build?
