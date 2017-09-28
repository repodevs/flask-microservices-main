# FLASK MICROSERVICES

[![Build Status](https://travis-ci.org/repodevs/flask-microservices-main.svg?branch=master)](https://travis-ci.org/repodevs/flask-microservices-main)

This project is based on [testdriven.io](http://testdriven.io/) Microservices with Docker, Flask and React  

### Structure
1. _[flask-microservices-main](https://github.com/repodevs/flask-microservices-main)_ Docker Compose files, Nginx, admin scripts
2. _[flask-microservices-users](https://github.com/repodevs/flask-microservices-users)_ Flask App
3. _[flask-microservices-client](https://github.com/repodevs/flask-microservices-client)_ client-side based on ReactJS
---

## How To Run
----
### Build for Local 
1. create docker-machine for local (with virtualbox driver)
```bash
$ docker-machine create --driver virtualbox dev
```
2. activate docker-machine 
```bash
$ eval $(docker-machine env dev)
```
3. Build the images and spin up the containers
```bash
$ docker-compose up -d --build
```
4. create and seed the db then run the tests
```bash
$ docker-compose run users-service python manage.py recreate_db
$ docker-compose run users-service python manage.py seed_db
$ docker-compose run users-service python manage.py test
```

Test it by opening your browser [http://0.0.0.0:80](0.0.0.0:80) or [http://0.0.0.0:80/users](0.0.0.0:80/users) 

---
### Build for Production 

1. create docker-machine for production (with driver digitalocean based on ubuntu 14.04)   
```bash
$ docker-machine create --driver digitalocean --digitalocean-access-token=DO_TOKEN --digitalocean-image ubuntu-14-04-x64 prod
```
2. activate docker-machine   
```bash
$ eval "$(docker-machine env prod)"
```
3. Build the images and spin up the containers
```bash
$ docker-compose -f docker-compose-prod.yml up -d --build
```
4. create and seed the db then run the tests
```bash
$ docker-compose -f docker-compose-prod.yml run users-service python manage.py recreate_db
$ docker-compose -f docker-compose-prod.yml run users-service python manage.py seed_db
$ docker-compose -f docker-compose-prod.yml run users-service python manage.py test
```
5. watch the logs
```bash
$ docker-compose logs -f users-service
```
6. grab ip
```bash
$ docker-machine ip prod
```

Test it by opening your browser [http://YOUR_PROD_IP:80](YOUR_PROD_IP:80) or [http://YOUR_PROD_IP:80/users](YOUR_PROD_IP:80/users) 

----
## Other Commands

To stop Docker container:
```bash
$ docker-compose stop
```
To bring down the container:
```bash
$ docker-compose down
```
Force build:
```bash
$ docker-compose build --no-cache
```
Remove image:
```bash
$ docker rmi $(docker images -q)
```
---
Access database via psql:
```bash
$ docker exec -ti users-db psql -U postgres -W
```

