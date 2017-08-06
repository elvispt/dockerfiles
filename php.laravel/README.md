# Laravel ready Dockerfile

This image is ready to run a laravel installation.

Base image: php:apache. Take a look at the [docker store](https://store.docker.com/images/php).

## Packages added from base image:
* nano-tiny
* git
* zlib1g-dev
* libmemcached-dev

## PHP Extensions added
* zip
* pdo_mysql
* memcached (pecl)
* igbinary (pecl)

Installed:
* composer
* nodejs 8.*.*

Cleared apt cache, man pages, composer cache, pecl cache.

## How to use

### Building image.

Assuming you are in the Dockerfile directory:

`docker build -t <CONTAINER:TAG_NAME> .`

### Creating a container:

#### Basic
`docker run -dit --name <CONTAINER_NAME> -p 80:80 <IMAGE:TAG>`

#### Sharing volumes.

Assuming you want to share the current directory:

`docker run -dit --name <CONTAINER_NAME> -p 80:80 -v $PWD:/var/www/html:cached <IMAGE:TAG>`

### Create a base laravel app:

If you are just testing, or starting you laravel app, remember to install it first:
* Enter you container: `docker exec -it <CONTAINER_NAME> bash`
* Go to folder: `/var/www/html`
* Run command: `composer create-project --prefer-dist laravel/laravel .`

Go to your browser (localhost) and take a look. You might need to set proper permissions on the log folders created.
