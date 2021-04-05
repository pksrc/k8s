```
# build from dockerfile
docker build .

#build a docker image and tag it
docker build --tag bulletinboard:1.0 . 

# run the container
docker run -p 8000:80 -d --name pkginx nginx-pk:1.0

```

```
# show all images
docker images

# show images with a "pattern"
docker images -a |  grep "pattern"

# show dangling images
docker images -f dangling=true
```

```
# clean up dangling
docker system prune
#docker rmi $(docker images --filter "dangling=true" -q --no-trunc) #Remove dangling/tags=<none> images

# clean up all
docker system prune -a

#clean up specific image
docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
```

```
# show all docker containers
docker ps -a

# show containers with a pattern
docker ps -a |  grep "pattern”

# show all exited containers
docker ps -a -f status=exited
docker ps -a -f status=exited -f status=created
```

```
# remove comtainer 
docker rm ID_or_Name ID_or_Name

# remove container with a pattern
docker ps -a | grep "pattern" | awk '{print $1}' | xargs docker rm

# remove all exited containers
docker rm $(docker ps -a -f status=exited -q)
docker rm $(docker ps -a -f status=exited -f status=created -q)
```