# Docker

command :
```
    // --help

    docker run [command]
    docker network [command]
    
    docker container create [image:tag]
    docker ps //actively running container
    docker ps --all //all container stop/start -a

    docker logs [name container]
    docker container start --attach [name container]
    docker kill [name container or id]

    docker exec --interactive --tty [name or id container] bash //for debug your apps
    docekr exec -i --y [name or id container] bash
```
---

## Easy way run docker container :
docker run a combination of :
- docker container create
- docker container start
- docker container attach

```
    docker run hello-world:linux
```

#### doing with Dockerfile :
```
    //will search file Dockerfile in your directory
    docker build -t our-first-image . // -t tag name of your image in your docker file 
    
    //or if you wanted to use file name in your Dockerfile you also can do this
    docker build -t our-first-image --file production.Dockerfile .    //will search dockerfile name --file or -f
    //and you must be notice if you are use path directory in your path like /app/src/config/ in your docker file

    //run
    docker run our-first-image //corelated with name your image when you naming in build 
```

but this is the fun fact, you will run with your terminal and cannot stop because forgot somenthing 
lets fix this with :
```
    docker run -d our-first-image // -d indicate docker will running on your background machine
    docker run -d -it our-first-image //you can also debug for this container -it --interactive tty
    docker run -it -d -p 5000:5000 -v ${PWD}:/app/code our-first-image

    //dont forget to use this -d its your ninja ways !!!
```
---

REMOVE container :
```
    docker stop [name or id container]
    docker stop -t 0 [name or id container] //becareful this will lost your data (force close immediatly) -t --time int it means you are run 0 int time, immediately

    docker rm [name or id]
    //or easy way, you wanted to stop and also remove container
    docker rm -f [name or id]

    //and this is for remove all your docker container (warning !!!!)
    docker ps -aq | xargs docker rm

```

---

REMOVE images :
```
    docker images //this is list all images in your docker
    docker rmi [name of images:tags]

```
fun fact you cannot remove if container image still running.

---

Binding port in your container :
```
    // -t name or tag your build image
    docker build -t your-image-build -f your-dockerfile.Dockerfile
    //5001 your actually computer and 5000 your apps running
    docker run -d --name your-name-container -p 5001:5000 your-image-build
    docker logs your-name-container // make sure your docker container running
```
---

SAVE DATA in your container :
```
    // -v or --volume
    docker run -d --name your-name-container -v /tmp/container:/tmp -p 5001:5000 your-image-build
```

---
---
---
---


## Docker HUB

### Push your Images into DockerHub
you must login into docker hub : docker login

1. Rename your image with your current username
```
    docker tag (your-current-images-on local machine) (your-username/(new-image-to push into dockerhub):tag version)
    docker tag server-express ucup/server-express:1.0

```

2. Push into docker hub
```
    docker push ucup/server-express:1.0 
```

---

```

docker run -d --name website -v "$PWD/website:/usr/share/nginx/html" -p 8080:8080 --rm nginx

```


---
note :
```
combination of :
- docker container create
- docker container start
- docker container attach
  
  docker run
```

docker run helpful :
```
docker run -it [container name]
docker run -it app  //indicate you will have mode --interactive and --tty so you can debug your container on docker
```

Search image in DockerHub:
```
docker search [name image]
docker search nginx
docker search --filter is-official=true nginx
```

fun fact :
- you can use your visual studio code and inspect your container, just right click and inspect your container