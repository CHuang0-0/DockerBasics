## Container Networking
###### containers are isolated by default
###### specify internal & external ports
```
docker run --rm -ti -p 45678:45678 -p 45679:45979 --name echoserver ubuntu:latest bash
```
###### data will get into one port, pass between 2 programs within the same container, then spit out of another port
###### install netcat
```
apt-get update && apt-get install -y netcat
```
###### nc: netcat; lp:listen port
```
nc -lp 45678 | nc -lp 45679
```
###### in terminal 2
```
nc localhost 45678
```
###### in terminal 3
```
nc localhost 45679
```
###### if nc not installed locally, refer to hosts
docker run --rm -ti ubuntu:14.04 bash
###### on mac:
```
nc <b>host:docker.internal</b> 45678
nc host:docker.internal 45679
```

## Exposing ports dynamically
###### containers to share the same hosts
###### let docker choose outside ports; only specify inside ports
```
docker run --rm -ti -p 45678 -p 45679 --name echoserver ubuntu:14.04 bash
nc -lp 45678 | nc -lp 45679
```
###### check dynamically generated external hosts
docker port echoserver
```
nc localhost <dynamic host #>
```

###### TCP or UDP
###### docker run -o outside-port:inside-port/protocal (tcp/udp)
###### e.g. docker run -p 1234:1234/udp
```
docker run --rm -ti -p 45678/udp --name echoserver ubuntu:14.04 bash
nc -ulp 45678
```
###### in terminal 2
```
docker port echoserver
nc -u localhost 52318
```

###### Connecting directly between containers
###### bridge: no specification
###### host: no network isolation/security concerns
###### none: no networking
```
docker network ls
docker network create learning
docker run --rm -ti --net learning --name catserver ubuntu:14.04 bash
docker run --rm -ti --net learning --name dogserver ubuntu:14.04 bash
nc -lp 1234
woof
```

## Legacy linking
##### one directional; depends on the order
```
// env var
docker run --rm -ti -e SECRET=wildcats --name catserver ubuntu:14.04 bash
nc -lp 1234

docker run --rm -ti --link catserver --name dogserver ubuntu:14.04 bash
nc catserver 1234
woof

env
```

## Listing images
```
docker images

// docker commit tags img for u
docker ps -l
docker commit <id> <img name>:<tag>
docker commit 61595668d26d myimg1
```
## remove imges
```
docker rmi <img name>:<tag>
docker rmi <img id>
docker rmi myimg1:latest
// remove stopped container first
docker rm ede960fdf094
docker rmi 929efa01f1
// force rmi
docker rmi -f f567a9b8e3
docker rm 5ef81b1486d8
```

## Sharing data with containers
##### sharing folder (persistent)
```
cd LearnDocker
mkdir example
cd example
docker run -ti -v /Users/celia.huang/LearnDocker/example:/shared-folder ubuntu bash
touch /shared-folder/my-data
ls /shared-folder/
exit
ls example/
// data survives expiration of containers
```
##### sharing files (--volumes-from:emphemoral)
```
// make sure files exist before containers
// create a volume not shared with the host
docker run -ti -v /Users/celia.huang/LearnDocker/shared-data ubuntu bash
cd ..
echo hello celia > shared-data/data-file

// shared discs that exist only as long as being
used
docker ps -l
docker run -ti --volumes-from friendly_antonelli ubuntu bash
ls /Users/celia.huang/LearnDocker/shared-data/
echo more >shared-data/more-data
ls shared-data
```

###### Docker registries
```
docker search ubuntu
docker login
docker pull debian:sid
// new name
docker tag debian:sid <login name>/testimg:v1.1
docker push <login name>/testimg:v1.1
```











