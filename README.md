# Laravel with Docker

## API

- It stands for **Application Programming Interface**.

- Set of definitions and protocols.

- Bridge between services. 

There are different standards to implement it.

- **SOAP** => Simple Object Access Protocol

- **GraphQL** => Graph Query Language

- **REST** => Representational State Transfer

## 6 Guiding Constraints for the REST API

1. Client Server Architecture

2. Statelessness

3. Cacheability

4. Layered System

5. Code on Demand

6. Uniform Interface


## Why API is Needed

1. Fetch Data.

2. Communicate with another machine.

3. Hide complexity.

4. Build dynamic applications.

5. Extend the functionality of a service or an app.

## Installing PHP, MYSQL and Composer on Windows

https://www.youtube.com/watch?v=3EC9WFagbYE

## Setup Laravel Environment with Docker

1. Install docker

2. Create your project folder, get into it and open the folder in your favourite IDE (In my case, VSCode | PHPStorm)

```
mkdir laravel_with_docker
cd laravel_with_docker
code .
```

3. Create a `docker-compose.yml` file

![Screenshot 2024-08-10 at 4 59 27 PM](https://github.com/user-attachments/assets/9eab14a9-3a7b-44dc-a6f3-447d72e8b9b2)

4. You need to have the following images in your docker file for it to work.

i) PHP with apache - https://hub.docker.com/_/php

ii) DB/Mariadb (Mysql in my case) - https://hub.docker.com/_/mysql, https://hub.docker.com/_/mariadb

iii) phpmyadmin (optional) to easily access the DB without any external tool such as DataGrip from JetBrains - https://hub.docker.com/_/phpmyadmin

iv) Need to set a volume for the DB to store the DB persistently

v) Need to set a network so that all of the above three images communicate with each other

With the PHP, we need to make some additional stuff e.g,

- setup working directory in the image => code will be in our local/host system, but we need to copy that

```
version: '3.9'

services:
  db:
    image: mariadb
    restart: unless-stopped
    volumes:
      - db_data:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD_FILE=/run/secrets/db_root_password
      - MYSQL_DATABASE=docker_laravel
      - MYSQL_USER=docker_laravel
      - MYSQL_PASSWORD_FILE=/run/secrets/db_password
    secrets:
      - db_root_password
      - db_password
    networks:
      - docker_laravel
  
  phpmyadmin:
    image: phpmyadmin
    restart: unless-stopped
    depends_on:
      - db
    ports:
      - "8080:80"
    environment:
      - PMA_HOST=db
      - MYSQL_ROOT_PASSWORD_FILE=/run/secrets/db_root_password
    secrets:
      - db_root_password
    networks:
      - docker_laravel

secrets:
  db_password:
    file: db_password.txt
  db_root_password:
    file: db_root_password.txt

volumes:
  db_data:

networks:
  docker_laravel:
    driver: bridge
```

### Start the container

```
docker-compose up
docker compose up -d # run in detach mode
```

### End the container
```
docker-compose down
```



## Creating Laravel Application

`composer create-project laravel/laravel example-app`

## Staring Laravel Application

`php artisan serve`

## Project Structure


![Screenshot_16](https://user-images.githubusercontent.com/204423/207503735-27defceb-2989-45e5-b9fb-60c6c38f7ee8.png)


## Configuring DB

You do it in the `.env` file.


![Screenshot_15](https://user-images.githubusercontent.com/204423/207367579-c5d9378f-f6d7-42e1-ae07-42a077e1f17e.png)

## What you need to make an API

- Model

- Migration

- Controller

- API resource

- Factory

- Seeder

### Model

- Each table in the DB has a corresponding Model class in the laravel application.

- It's used to do CRUD operations on the table.

- The convention is to name it `Singular`.

- You can create a model with the following command

```
php artisan make:model ModelName 
```

- You can create, migrate, Factory, Seeder and Controller with Model, too.

```
php artisan make:model ModelName -m
php artisan make:model ModelName --migration

php artisan make:model ModelName -f
php artisan make:model ModelName --factory

php artisan make:model ModelName -s
php artisan make:model ModelName --seed

php artisan make:model ModelName -c
php artisan make:model ModelName --controller

php artisan make:model ModelName -mfsc
php artisan make:model ModelName --migration --factory --seed --controller

// This one will create migration, factory, seeder and controller in one command.
php artisan make:model ModelName -a
php artisan make:model ModelName --all


```

### Migration



### Factor

```

```

### Seeder

```

```

### Controller

```
php artisan make:controller PhotoController

```

### API controller vs Standard Resource Controller

- API controller routes don't use `create` and `edit` methods

- We can create a controller which excludes those 2 methods using the `--api` flag.

```
php artisan make:controller PhotoController --api

```

- To use Controller, Model, and Route binding, use `--model` flag when creating controller

```
php artisan make:controller PetitionController --api --model=Petition

```

![Screenshot_17](https://user-images.githubusercontent.com/204423/207511193-ead5178f-7fb1-41cb-9f6b-998af034806c.png)


### API Resource

- These are the template classes where you defined how you want the JSON data to be returned to the user.
- You create these resources for a single collection and for any other type of resource you want to return.

```
php artisan make:resource PetitionResource

php artisan make:resource PetitionCollection // Create a collection resource. I figure that out from the name.
```




# Reference

- https://laracasts.com/
- https://laravel.com/docs/
- https://laravel-news.com/
- https://laravelpodcast.com/

## Tutorial Websites
- https://www.larashout.com/
- https://www.tutsmake.com/category/laravel-tutorial/
- https://www.tutorialspoint.com/laravel/index.htm
- https://bitfumes.com/
- https://learn2torials.com/category/laravel

## Youtube Channels

- https://www.youtube.com/c/LaravelDaily/featured
- https://www.laraning.com/
- https://www.youtube.com/watch?v=ImtZ5yENzgE
- https://www.youtube.com/watch?v=30qk04BG9G4


## Opensource Projects

- https://github.com/monicahq/monica
- https://github.com/koel/koel
- https://github.com/flarum
- https://github.com/invoiceninja/invoiceninja
- https://github.com/crater-invoice/crater
- https://github.com/akaunting/akaunting
- https://github.com/bagisto/bagisto
- https://devdojo.com/wave
- https://github.com/pterodactyl/panel
- https://github.com/pixelfed/pixelfed
- https://github.com/orchidsoftware/platform
- https://github.com/nuwave/lighthouse
- https://github.com/arashactive/laramint

