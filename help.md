### When you cannot create more container :
Solution 1 :
```
    docker images //list all your images first
    docker images rmi (your images) (your images) (your images)
    or
    docker images rmi -f (your images) (your images) (your images) //data will lost warning
    docker rmi -f $(docker images -f "dangling=true" -q)
```

Solution 2 :
```
    docker system prune //will stop all container network etc
```

### When your docker run slowly :
```
    docker stats
    docker inspect (name container) | less
    docker top [container-id]

```
and you can see how process in your docker file incorect

---
---
---
FUN FACT :

1. always use verified docker images
2. container images scanner
   -clair
   -trivy
   -Dagda
3. avoid latest in tag when you push your images docker into docker hub

   - ucup/webserver:1.0.1 always version your image docker 
   - latest make rollback difficult
4. use non root in docker
5. docker compose will make better if you are lazy to know all command :D hahaha
   docker-compose up
   docker-compose down
6. kubernetes if you wanna running multiple container in production
   secure network
   any vm
   its about delivery service you can provide in kubernetes

### Docker Compose
1. Simplify local development by allowing you to run multiple containers at once.
2. Uses a manifest file to declare your application's dependencies and run them in a local Docker network.
3. Prevents you from having to run multiple docker CLI commands to start multiple containers.

### Kubernetes
Autoscaling containers and transparently moving them from machine to machine.
