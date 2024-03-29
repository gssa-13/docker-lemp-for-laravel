![license](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![GitHub tag checks state](https://img.shields.io/github/checks-status/gssa-13/docker-lemp-for-laravel/main?color=success&label=Branch%20state&style=flat-square)
![GitHub issues](https://img.shields.io/github/issues/gssa-13/docker-lemp-for-laravel?style=flat-square)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/gssa-13/docker-lemp-for-laravel?style=flat-square)
![GitHub repo size](https://img.shields.io/github/repo-size/gssa-13/docker-lemp-for-laravel?style=flat-square)
## Ubuntu, Nginx, PHP-FPM, Supervisord and Nodejs for Laravel

## Software versions
|Lavarel | Ubuntu | Nginx | PHP   | Composer | NodeJs | Mysql | MariaDB | Redis |
|--------|--------|-------|-------|----------|--------|-------|---------|-------|
| 9.*    | 22.04  |  1.18 | 8.1.* |  Latest  | 18.6.0 |8.0.30 | 10.9.2  | redis:7.0.4-alpine3.16 |


## Installation
### New Project
After to download laravel, you need copy this repository files to the root directory of your Laravel application
```
| Laravel app
 -----| app
 -----| public
 -----| 'docker'
 -----| 'develop'
 -----| 'docker-compose.yml'
```

#### First step

First at all, you have to export your user and group ID in your shell configuration
``` shell
$ export USER_ID=$(id -u)
$ export GROUP_ID=$(id -g)
```

#### Run docker compose
To build and run the application like `docker compose up -d`
``` shell
$ ./develop start
```
#### Install composer dependencies
Is needed install composer dependencies for laravel runs
``` shell
$ ./develop composer install
```
#### Generate app key
Generate your application encryption key using the following command
``` shell
$ ./develop artisan key:generate
```

## Define environment variables
If it's a new project, copy your `.env.example` file to `.env`
  substitute the following data as  convenient to use on your local machine
* MySQL or MariaDB data
``` 
DB_HOST=127.0.0.1 => DB_HOST=mysql || DB_HOST=mariadb
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=username
DB_PASSWORD=secret
```

* Redis
```
REDIS_HOST=127.0.0.1 => REDIS_HOST=redis
REDIS_PORT=6379
```

## Usage
To build and run the application like `docker compose up -d`
``` shell
$ ./develop start
```
To list all containers like `compose ps`
``` shell
$ ./develop
```
To stop containers like `docker compose down`
``` shell
$ ./develop stop
```
To run artisan command like `php artisan :command`
``` shell
$ ./develop artisan :command
$ ./develop art :command
```
To execute compoer like `composer require predis/predis`
``` shell
$ ./develop composer predis/predis
$ ./develop comp predis/predis
```
To run phpunit tests from `./vendor/bin/phpunit`
``` shell
$ ./develop test :test_name
```
To run yarn commands
``` shell
./develop yarn :command
```
To run npm commands
``` shell
./develop npm :command
```
To run gulp commands from `./vendor/bin/phpunit`
``` shell
./develop gulp :command
```

## License

This software is licensed under the [MIT license](https://opensource.org/licenses/MIT).
