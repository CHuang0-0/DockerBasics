## Dockerfile
##### caching with each step
##### skip lines unchanged since the last time
##### not shell scripts
##### processes on one line will not run on the next
##### use ENV to export env variables
```
docker build -t <tag> . <path>
```

## Building Images
##### create a docker file
```
cd /users/celia.huang/learndocker/example
nano Dockerfile
------
FROM busybox   // create an image
RUN echo "buiding celia's docker img"  // create a container and run
CMD echo "hello container"   // echo in the container
------
ls
docker build -t hello .
docker run --rm hello
```
##### install a program with docker build
```
nano Dockerfile
-----
FROM debian:sid
RUN apt-get -y update
RUN apt-get install nano
CMD ["bin/nano","temp/notes"]
-----
docker build -t nanoer .
// cmd to run is baked into img
docker run --rm -ti nanoer
```
##### add a file via docker build
```
nano Dockfile
-----
FROM example/nanoer
Add notes.txt /notes.txt
CMD ["/bin/nano","/notes.txt"]
-----
nano notes.txt
docker build -t notes .
docker run -ti --rm example/notes
```

## Dockerfile Syntax
```
// from what image
FROM  <img>

// authoer
MAINTAINER <name> <email address>

// run
RUN unzup <zip file><dir>
RUN echo hello

// add
ADD run.sh /run.sh
ADD <content>
ADD <urls>

// ENV
ENV db_port=123

// entrypoint: start of the cmd to run
// cmd: the whole cmd to run

// expose a port into a conainer
EXPOSE 8080

// volume
VOLUME ["/host/path/" "container/path/"]

// workdir sets dir for containers to start
WORKDIR /path/

// user: run as
USER celia
```

## Golden Img Problem
##### include multiple FROM statements
##### preserve the ability to create a reproducible build


## Golden Img Problem
##### include installer
##### build from scratch
##### small img like Alphine















