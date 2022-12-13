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
Build and run the container in background
```
docker-compose up --build --scale nodeserver=2 -d
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
```
docker rmi $(docker images -a -q)
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

Try this command to get only error.log:
```
docker logs -f nginx 1>/dev/null
```
And this one for access.log:
```
docker logs -f nginx 2>/dev/null
```


```


Update July 1st 2019
docker-compose logs <name-of-service>
for all services

docker-compose logs
Use the following options from the documentation:

Usage: logs [options] [SERVICE...]

Options:

--no-color Produce monochrome output.

-f, --follow Follow log output.

-t, --timestamps Show timestamps.

--tail="all" Number of lines to show from the end of the logs for each container.



13 DEC 2022 #Issue arised - NGINX port 80 bind
resolved by stoping GCP nginx. 

location- cd /etc/nginx

cmd: 

  639  sudo systemctl start nginx
  640  sudo systemctl status nginx
  641  sudo systemctl stop nginx
  642  sudo systemctl status nginx
  644  sudo docker-compose up --build --scale nodeserver=5 -d


```