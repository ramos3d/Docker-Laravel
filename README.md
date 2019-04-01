# Docker-Laravel 5.8
This is a very simple Docker image running:
* Laravel 5.8
* Nginx
* PHP 7.1
* MySQL 5

# Example

- Ports 8888: http://localhost:8888

# Generating your own Docker Composer
Access https://phpdocker.io/generator and do the following steps:

## Step 1
### Global Configuration 
- Project Name: your_project_name
- Application Type: Generic Synfony 4, Zend, Laravel ...
- Base port: 8888 //but feel free to choose anyone

### PHP Configuration
- PHP Version: 7.1x
- Extensions (PHP 7.1x): MySQL, Redis

### MySQL
- Enable MySQL: Turn On
... Fill out the form with standard values, but they can be changed later.

### Zero-Config Services
- Enable Redis: Turn On

Click on **Generate project archive**

## Step 2

Do unpack the file generated in your folder, e.g. (/var/www/html/ramos3d/)
Access the **phpdocker/** folder and start docker by typing:

```console 
docker-compose up -d
```
If everything is good, now the container will up.

## Step 3
Creating a new session bash of this container

```console
docker exec -it nameOfYourFolder-php-fpm /bin/bash

```
Once inside the container, it is time to install the Laravel framework via composer

## Step 4
```console
composer create-project --prefer-dist laravel/laravel src
```
Leave it and Stop the container after Laravel installation is complete by typing:
```console
# CTR+C
# docker-compose stop
```

Enabling permissions to write

```console
# chown yourUser:yourUser -R ../src

```
## Step 5

Check the file **docker-compose.yml**, it is possible that you have to change the line 
volumes: 
  .:/application 
To
volumes:
 ./src:/application
 
 Do this in both **webserver** and **php-fpm**
 
 ```console
 sudo chmod -R 777 ../src/
 docker-compose up -d
 ```
 Attention: **DO NOT USE** 777 on production server for security reasons. 
 ## It is Done
 
