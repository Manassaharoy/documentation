# Docker installation and setup

#### Steps to create and run a docker container

- Install docker hub in mac/windows
- run the docker hub

</br>

```
we have used docker compose, but to run a single dockerfile bellow command have to be used

docker run -p 80:<PORT> <containername>
```
</br>


- go to the folder that contains the "docker-compose.yml" file and use the following commands:
(if docker-compose is not installed then install it)

</br>


To start the dockerizing process and running the container
```
docker-compose up
```
or to rebuild from cached images
```
docker-compose up
```
Build and run the container in background
```
docker-compose up -d
```
Stop the container
```
docker-compose stop
```
Stop and delete the container
```
docker-compose down
```

</br>

To check the running images list 
```
docker image ls
```
Delete an image
```
sudo docker rm image <ID> -f
```
Delete all unused images
```
docker image prune -f
``` 

</br>

To check container list
```
docker ps -a 
``` 
or 
```
docker-compose ps
```

