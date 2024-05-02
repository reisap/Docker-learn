### Docker Compose
type of environment is suited to use Docker Compose
1. test
2. development / staging
3. local
   
IS NOT FOR PRODUCTION MODE !!!!

---

```
docker-compose up   //docker-compose build && docker-compose create && docker-compose start
docker-compose down
docker-compose start
docker-compose stop
```

### Environment
only use when you are first build this apps, the value set in the shell bash sh

sample :
```yaml
services:
  scheduler:
    environment:
      - runtime_env=local
  storefront:
    environment:
      - runtime_env=local
```
it can not run on container so its different purpose | runtime_env=local npm run start | like you are using in first apps

---
---

### Volumes
```

//create volume name for docker compose, so you are not running with random machine volume for docker compose up/start
    database:
        //....////
        volumes:
            - apps-express : /var/lib/mysql:rw   //rw read write ro -> read only
volumes :
    apps-express:

```
example :
``` yaml

version: "3.9"

services:
  scheduler:
    build: scheduler/.
    ports:
      - "81:80"
    depends_on:
      - database
  storefront: 
    build: storefront/.
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - database
  database: 
    image: "mysql:${TAG}"
    env_file:
      - ./mysql/env_vars
    volumes:
      - ./mysql:/docker-entrypoint-initdb.d:ro #indicate read only rw == read and write
      - kineteco:/var/lib/mysql
volumes:
  kineteco: 

```

### Service profile
for spesific profile on frontend or backend
``` yaml
version: "3.9"

services:
  scheduler:
    build: scheduler/.
    ports:
      - "81:80"
    depends_on:
      - database
    profiles:
      - scheduling_services
  storefront: 
    build: storefront/.
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - database
    profiles:
      - scheduling_services
  database: 
    image: "mysql"
    env_file:
      - ./mysql/env_vars
    volumes:
      - ./mysql:/docker-entrypoint-initdb.d:ro
      - kineteco:/var/lib/mysql
    # profiles:
    #   - scheduling_services
volumes:
  kineteco: 
```
 profiles: its indicate you are have a name for your spesific service and you can run with : 

 docker-compose --profile [name profile in docker-compose.yaml]

 //sample
```
 //it will running only for frontend,, database and backend not running
 docker-compose --profile scheduling_services up 
 docker-compose --profile scheduling_services down
 docker-compose --profile scheduling_services restart
 docker-compose --profile scheduling_services stop
```
----

### Name Docker Compose
the goal is :
1. having multiple compose files for independent versions of an application
2. having multiple compose files for different environments, such as local and staging

```
docker-compose -f docker-compose.local.yaml -f docker-compose.yaml 
//it will using only for first build, so you can run on different purpose like local, testing or production
//remember about Environment its different between env_file
```

### Run with name different env file
docker-compose --env-file [path]
docker-compose --env-file production.env

or you can use in your docker-compose.yaml
``` yaml
version: "3.9"

services:
  scheduler:
    build: scheduler/.
    ports:
      - "81:80"
    depends_on:
      - database
  storefront: 
    build: storefront/.
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - database
  database: 
    image: "mysql"
    env_file: #indicate you are using your env file
      - ./mysql/env_vars
    volumes:
      - ./mysql:/docker-entrypoint-initdb.d:ro
      - kineteco:/var/lib/mysql
volumes:
  kineteco: 
```

