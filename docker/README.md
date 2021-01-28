### docker build
    docker-compose build php

### create project (e.g. laravel
    docker-compose run --rm --no-deps php composer create-project laravel/laravel .

### docker container start (with deps)
    docker-compose up -d nginx

### container login
    docker-compose exec php ash

### container logs (nginx)
    docker-compose logs -f nginx