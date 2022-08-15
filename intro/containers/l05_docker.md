```
docker ps     = docker container ls  
docker images = docker image ls  
  
docker build .  
  or    
docker build <dockerfile>   
  
docker pull nginx       pulls image  
docker run              pulls and runs image  
docker start            starts existing container  
  
docker volume create <volume name>  
docker volume ls  
docker volume inspect <volume name>  
```

== PORTS:==
```
exposed port - opens port in container, available to local services 
published port -- accessible from outside
```
```
docker run -P nginx
publishes exposed port 80 as random ethereal port (i.e. 49153)
```
== volumes ==

create volume
```
docker volume create dev_volume  
docker volume ls  
docker volume inspect dev_volume
```

create container
```
docker container run -d -P --name my_dev_container --mount source=dev_volume,target=/app nginx  
docker container inspect my_dev_container | jq '.[0].Mounts[0].Source'
>>>"/var/lib/docker/volumes/dev_volume/_data"
not accessible
```

add file to volume
```
docker container exec -it my_dev_container bash
echo "hello" >> /app/hello.txt
``` 

mount to another container
```
docker container run -d -P --name my_dev_container_2 -v dev_volume:/app nginx  
```
