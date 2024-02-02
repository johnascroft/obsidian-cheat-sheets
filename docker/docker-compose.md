# Docker Compose
  
A `docker-compose.yml` file stores the services that are required for your application. You would have [[nginx]] as a service, [[php]] as a service, [[mysql]] as a service etc. Running `docker-compose up` will start up all those services as containers.  
  
This will bring all containers up, but run it in the background (`-d` flag)  

```bash  
docker-compose up -d
```

Log in to the [Docker Hub](https://hub.docker.com/)  

```bash
docker login
```  
  
You can run any Docker image from the Docker Hub repo  

```bash  
docker run <image>
docker run tutum/hello-world
docker run -p 8080:80 tutum/hello-world // exposes port 80 on the container to port 8080 publicly
```  
  
This will show all the containers (the `-a` shows all, including those that are stopped)  

```bash  
docker ps -a
```  
  
Removes a docker container  

```bash  
docker rm <id>
```  
  
Creating multiple instances, creating a name for each of them (`web1`, `web2`, `web3` etc)  

```bash  
docker run -d --name web1 -p 8081:80 tutum/hello-world
docker run -d --name web2 -p 8082:80 tutum/hello-world
docker run -d --name web3 -p 8083:80 tutum/hello-world
```

List the active containers :

```bash
docker ps
```

Stop a container by name

```bash
docker stop web3
```