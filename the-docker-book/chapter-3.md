# Docker 3: Getting Started with Docker
- `docker info`
  - check if docker binary works
  - returns containers, images, storage drivers docker is using and basic config

### Creating Containers
- `docker run -i -t ubuntu /bin/bash`
  - creates a container
    - use `create` to create without running
  - provides two things we need for interactive shell in new container
    - -i keeps STDIN open from the container even if not attached
    - -t tells docker to assign a tty to the container
  - told docker to use ubuntu base image
    - checks locally for image before connecting to registry
  - new container has network, IP address, bridge interface
  - docker runs a bash shell in it and logs us in as root
  - container is an ubuntu host that can do ubuntu things
  - be cool: install vim

### Killing Containers
- container runs as long as command argument runs
  - `exit` stops command and container
  - container still exists
  - `docker ps` shows running contianers
  - -a flag shows all
  - -l shows last container info
  - -n x shows last x containers, running or stopped
- `docker rm container_name` removes containers

### Restarting Containers
- docker generates random unique names for our containers
  - can use --name to define your own name
  - can use instead of id for most commands
- `docker start container_name` restarts
  - uses same options from `run` command
- `docker attach container_name` gets you back into session

### Longlasting Containers
- daemonized containers don't have interactive sessions but are ideal for running things
- `docker run --name container_name -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`
  - -d detaches container to background
  - while loop keeps the party going
  - command returns us to prompt instead of attaching

### Logs
- `docker logs container_name`
  - outputs last few log entries
  - -f to monitor
  - -t for timestamps
  - --tail x is last x lines
  - ctrl-c to exit
- --log-driver option to daemon and docker run to set output prefs
  - can send to syslog which disables logs command
  - can set to none and disable logs command

### Processes
- `docker top container_name` shows processes, user, pid
- `docker states container1 container2` shows CPU, memory, network I/O

### Running Processes in Containers
- background and interactive types
- `docker exec -d container_name touch /etc/new_config_file`
  - -d flag for background process, container name and process
  - can run maintenance, monitoring or management inside containers
- `docker exec -t -i container_name /bin/bash`
  - a shell! so interactive

### Stop the Demons
- `docker stop container_name` sends SIGTERM to running processes
- `docker kill` sends SIGKILL

### Auto Restarts
- `docker run --restart=always --name container_name -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`
  - will attempt to restart always
  - on-failure takes optional argument of restart count

### Getting to Know Your Container
- `docker inspect container_name`
  - returns names, commands, networking configuration
- `docker inspect --format='{{ .NetworkSettings.IPAddress }}' container1 container2`
  - --f or --format selectively returns results

### Destroy All
- "docker rm -f `sudo docker ps -a -q`"
  - returns list of container ids for docker to remove
  - -f force removes running containers
