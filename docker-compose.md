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

### Service profile
for spesific profile on frontend or backend

### Name Docker Compose
docker-compose -f docker-compose.local.yaml -f docker-compose.yaml

### Run with name different env file
docker-compose --env-file [path]
docker-compose --env-file production.env

