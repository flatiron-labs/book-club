# Docker test a static website using nginx
1) They use the non-demonized nginx so logs will be pushed out.
2) They get into using volumes for development.
3) Testing is just done by loading the website locally.

# Testing web apps:
1) Build small sinatra app, run and test
2) They build their own redis image
    
## Getting into docker networking
### old way, docker internal networking
1) docker0 interface
2) veth interfaces

```
Every time Docker creates a container, it creates a pair of peer interfaces that are like opposite ends of a pipe (i.e., a packet sent on one will be received on theother). It gives one of the peers to the container to become its eth0 interface andkeeps the other peer, with a unique name like vethec6a, out on the host machine.You can think of a veth interface as one end of a virtual network cable. One end isplugged into the docker0 bridge, and the other end is plugged into the container.By binding every veth* interface to the docker0 bridge, Docker creates a virtualsubnet shared between the host machine and every Docker container.
```
### new way, Docker networking
#### Can create a network with a name
#### can add containers to that network and their given names are now resolvable in DNS.
#### docker-compose does all this for us.
####  we can add already running containers to already existing networks with docker network connect.

# Continuous integration
## installing jenkins.  Creating image and running with /var/run/docker.sock mounted.
## Created a jenkins job that will build a basic docker images.  We then mount the code during runtime and run rspec.  The way he is building containers is a little different than we are.  He builds very generic images without code, and then mounts code at runtime, but we add the code in during the build.
