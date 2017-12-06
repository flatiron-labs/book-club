# The Docker Book: Chapter 6

## Building Services with Docker

Goal: build "on-demand" Jekyll website.  
- served via Apache
- create new set when new container is launched

### Jekyll base image

TIL `vi Dockerfile` creates file

1. Updates, installs ruby, build-essential, node, jekyll gem
2. Creates 2 volumes

### Launching Jekyll site

I got some errors:

```bash
12:10:56 kLocal @ktravers: james_blog (master)
$ docker run -v $(pwd):/data/ --name james_blog jamtur01/jekyll
container_linux.go:265: starting container process caused "exec: \"jekyll\": executable file not found in $PATH"
docker: Error response from daemon: oci runtime error: container_linux.go:265: starting container process caused "exec: \"jekyll\": executable file not found in $PATH".
ERRO[0000] error waiting for container: context canceled
```

What is a volume? (p216)  
- designated directory inside one or more containers that bypasses Union File System (follow up question: what is the Union File System?)
- can be shared and reused between containers
- container doesn't have to be running to share volumes (!!)
- volumes persist even when no containers use them

Allows you to add data to an image w/o committing that data to the image.

Volumes live on Docker host at `/var/lib/docker/volumes`

Inspecting a volume:

```bash
12:11:04 kLocal @ktravers: james_blog (master)
$ docker inspect -f "{{ range .Mounts }}{{.}}{{end}}" james_blog
{bind  /Users/kLocal/Development/practice/james_blog /data   true rprivate}{volume 55f1364155563936ba9ce989481e291f22a240768ab8b9ad39a8643e289fc49a /var/lib/docker/volumes/55f1364155563936ba9ce989481e291f22a240768ab8b9ad39a8643e289fc49a/_data /var/www/html local  true }
```

### Extending our Jekyll website example

p222 Using Docker to build our own variant of GitHub Pages... useful for blogs?

### Fetching a WAR file

More errors:

```bash
12:26:54 kLocal @ktravers: fetcher
$ docker run -t -i --name sample jamtur01/fetcher \ https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war
 https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war: Scheme missing.
```

### Building on top of our Tomcat application server

Installing Sinatra app on Docker host vs. installing inside container?




