# PHP 7.4 with Phalcon 4.1.0 Dockerfile

Dockerfile is originally build from [webdevops/php:7.4](https://github.com/webdevops/Dockerfile/tree/master/docker/php-official/7.4) with partial nginx configuration from [webdevops/php-nginx:7.4](https://github.com/webdevops/Dockerfile/tree/master/docker/php-nginx/7.4).

**Original Dockerfiles updates:**
- **Phalcon** extension preinstalled and does not need separate installation *(solves phalcon installation freeze issue using Docker Toolbox)*
- Latest **nginx** version installed, `/index.php` routed to `/app/public/index.php`
- **Composer** installed
- **Xdebug** installed
- **mcedit** installed and configured to edit files via `edit` command using `modarin256` skin *(better compatibility using PHP Storm dark mode)*

**Latest release software versions:**

| Software | Version (docker image)                                           | Version (manual build)                                           |
| -------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| PHP      | [7.4.12](https://www.php.net/releases/7_4_0.php)                 | [7.4.* (latest stable)](https://www.php.net/releases/7_4_0.php)                  |
| Phalcon  | [4.1.0](https://github.com/phalcon/cphalcon/releases/tag/v4.1.0) | [4.1.0](https://github.com/phalcon/cphalcon/releases/tag/v4.1.0) |
| Nginx    | [1.19.5](https://nginx.org/)                                     | [latest stable](https://nginx.org/)                              |
| Xdebug   | [3.0.1 ](https://xdebug.org/download)                            | [latest stable](https://xdebug.org/download)                     |
| Composer | [2.0.6](https://getcomposer.org/download/)                       | [latest stable](https://getcomposer.org/download/)               |

#
## Using docker image

Use one of docker images:
1. `phpnotdead/phalcon:7.4-4.1.0` from docker.io (usually, faster pull time)
2. `docker.pkg.github.com/php-not-dead/phalcon-dockerfile/php7.4:4.1.0` from github.com

### Using docker-compose

```
image: phpnotdead/phalcon:7.4-4.1.0
```
Full `docker-compose.yml` file example with `7.4-4.1.0` release tag:
```
version: '3.7'
services:
  phalcon:
    container_name: phalcon
    image: phpnotdead/phalcon:7.4-4.1.0
    ports:
    - 801:80
    volumes:
    - ./src:/app
```

###
### Using docker pull & docker run

```
docker pull phpnotdead/phalcon:7.4-4.1.0
docker run -d -v src:/app -p 801:80 --name phalcon phpnotdead/phalcon:7.4-4.1.0
```

#
## Building docker image manually

### Add git repository to `docker-compose.yml` file `context`:

Using exact release tag (recommended):
```
context: https://github.com/php-not-dead/phalcon-dockerfile.git#release_tag
```
Using `master` branch:
```
context: https://github.com/php-not-dead/phalcon-dockerfile.git
```
Full `docker-compose.yml` file example with `7.4-4.1.0` release tag:
```
version: '3.7'
services:
  phalcon:
    container_name: phalcon
    build:
      context: https://github.com/php-not-dead/phalcon-dockerfile.git#7.4-4.1.0
    image: phalcon
    ports:
    - 801:80
    volumes:
    - ./src:/app
```

###
### git clone or download repository and add `docker-compose.yml` file:

Specify a path to `Dockerfile` in `context`:
```
context: '.'
```

###
### Use `docker run` command specifying full path to `Dockerfile`:

Run directly from git repository:
```
docker build https://github.com/php-not-dead/phalcon-dockerfile.git#7.4-4.1.0 -t phalcon
docker run -d -p 801:80 -v src:/app --name phalcon phalcon
```
-- OR --

`git clone` or download repository and run:
```
git clone https://github.com/php-not-dead/phalcon-dockerfile.git
docker build -t phalcon phalcon-dockerfile
docker run -d -v src:/app -p 801:80 --name phalcon phalcon
```
