# PHP 7.4 and Phalcon 4.0.6 Dockerfile

Dockerfile is originally build from [webdevops/php:7.4](https://github.com/webdevops/Dockerfile/tree/master/docker/php-official/7.4) with partial nginx configuration from [webdevops/php-nginx:7.4](https://github.com/webdevops/Dockerfile/tree/master/docker/php-nginx/7.4).

**Original Dockerfiles updates:**
- **Phalcon** extension preinstalled and does not need separate installation *(solves phalcon installation freezing using Docker Toolbox)*
- Latest **nginx** version installed, `/index.php` routed to `/app/public/index.php`
- **Composer** installed
- **Xdebug** installed
- **mcedit** installed and configured to edit files via `edit` command using `modarin256` skin *(better compatibility using PHP Storm dark mode)*

**Latest release software versions:**

| Software | Version                                                          |
| -------- | ---------------------------------------------------------------- |
| PHP      | [7.4.*](https://www.php.net/releases/7_4_0.php)                  |
| Phalcon  | [4.0.6](https://github.com/phalcon/cphalcon/releases/tag/v4.0.6) |
| Nginx    | [latest stable](https://nginx.org/)                              |
| Xdebug   | [latest stable](https://xdebug.org/download)                     |
| Composer | [latest stable](https://getcomposer.org/download/)               |

## How to use this Dockerfile

#### Add git repository to `docker-compose.yml` file `context`:

Using exact release tag (recommended):
```
context: https://github.com/php-not-dead/phalcon-dockerfile.git#release_tag
```
Using `master` branch:
```
context: https://github.com/php-not-dead/phalcon-dockerfile.git
```
Full `docker-compose.yml` file example with `7.4-4.0.6` release tag:
```
version: '3.7'
services:
  phalcon:
    container_name: phalcon
    build:
      context: https://github.com/php-not-dead/phalcon-dockerfile.git#7.4-4.0.6
      args:
      - APP_ENV=development
    image: phalcon
    ports:
    - 801:80
    volumes:
    - ./src:/app
```

#### `git clone` or download repository and add `docker-compose.yml` file:

Specify a path to `Dockerfile` in `context`:
```
context: '.'
```

#### Use `docker run` command specifying full path to `Dockerfile`:

Run directly from git repository:
```
docker build https://github.com/php-not-dead/phalcon-dockerfile.git#7.4-4.0.6 -t phalcon
docker run -d -p 801:80 -v src:/app --name phalcon phalcon
```
`git clone` or download repository and run:
```
git clone https://github.com/php-not-dead/phalcon-dockerfile.git
docker build -t phalcon .
docker run -d -v src:/app -p 801:80 --name phalcon phalcon
```
