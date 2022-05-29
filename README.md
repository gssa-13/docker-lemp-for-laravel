![license](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![GitHub tag checks state](https://img.shields.io/github/checks-status/gssa-13/docker-lemp-for-laravel/main?color=success&label=Branch%20state&style=flat-square)
![GitHub issues](https://img.shields.io/github/issues/gssa-13/docker-lemp-for-laravel?style=flat-square)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/gssa-13/docker-lemp-for-laravel?style=flat-square)
![GitHub repo size](https://img.shields.io/github/repo-size/gssa-13/docker-lemp-for-laravel?style=flat-square)
## Ubuntu, Nginx, PHP-FPM, Supervisord and Nodejs for Laravel

## Installation
Copy the repository files to the root directory of your Laravel application
```
| Laravel app
 -----| app
 -----| public
 -----| 'docker'
 -----| 'develop'
 -----| 'docker-compose.yml'
```

## Software versions
| Ubuntu | Nginx | PHP   | Composer | Nodejs |
|-------|-------|---------|--------|--------|
| 22.04  | 1.20  | 8.1.2 | Latest  | 18.2.0 |

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
$ ./develop artisan :command
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

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
