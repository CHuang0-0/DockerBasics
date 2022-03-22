## Hello World
```
docker run hello-world
```

## Go pretty print format
```
export FORMAT='ID:{{.ID}}\nImage:{{.Image}}\nCommand:{{.Command}}\nCreated:{{.CreatedAt}}\nStatus:{{.Status}}\nPorts:{{.Ports}}\nNames:{{.Names}}\n'
echo $FORMAT
```

## Images
```
docker images
```

## Running containers from images
###### terminal interactive
```
docker run -ti ubuntu:latest bash
ls
```
###### see the standard distr
```
cat /etc/lsb-release
exit (or <b>ctrl D</b>)
```
###### running images
###### images and containers have different ids
###### images are fixed when starting a container
```
docker ps
docker ps --format $FORMAT
```


## Stopped containers
###### see all containers
```
docker ps -a
```
###### see last containers to exit
```
docker ps -l
```


## Generate new images from stopped containers
```
docker run -ti ubuntu bash
ls
touch my_file
exit
docker ps -l
```
###### method 1
###### make images and get image ids
```
docker commit 82b9ba278444
```
###### give image names
```
docker tag sha256:f567a9b8e3f2f75ae3fee62283271ba66a336c8401a5b02d6f9e7b4f96215cc5 myimg
```
###### check image
```
docker images
docker run -ti myimg bash
ls
exit
```
###### method 2
```
docker commit "container name" "image name"
docker commit magical_nightingale myimg2
```
###### check image
```
docker images
docker run -ti myimg2 bash
ls
exit
```


## Docker Run
###### start a container for 2 secs then exit
```
docker run --rm ubuntu sleep 2
```
###### run container then echo
```
docker run -ti ubuntu bash -c "sleep 3; echo all done"
```
###### detach: leave containers running, prints out an id
```
docker run -d -ti ubuntu bash  ######id=1a8b6a87a1adb25b4f564a451b63cc48e4b7308d3f8fc760a969971fe618e79f
docker ps --format $FORMAT
```
###### jump into the container
```
docker attach recursing_cori
```
###### detach, keep running --> ctrl P, then ctrl Q

###### starts another process in an existing container
###### good for debugging
###### another shell in the container
###### do in an another terminal
```
docker exec -ti recursing_cori bash
ls
touch foo
ls
```


## Manage Containers
###### container output
```
docker logs "container name"
```
###### bug cmd
```
docker run --name example -d ubuntu bash -c "lose /etc/password"
```
###### debug
```
docker logs example
```

###### stop & remove containers
```
docker kill "container name"  // stop
docker rm "container name""   // be gone
docker run -ti ubuntu bash
```
###### in another terminal
```
docker ps --format=$FORMAT
docker kill laughing_aryabhata
docker ps -l --format=$FORMAT
docker rm laughing_aryabhata
```

###### Source Constaints
###### memory limits
```
docker run --memory="max memory allowed""
```
###### CPU limits
```
docker run --cpu-shares
docker run --cpu-quota
```

























