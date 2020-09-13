### Dockerfile with PHP 7.4 and Phalcon 4.0.6

Dockerfile is originally build from [webdevops/php:7.4](https://github.com/webdevops/Dockerfile/tree/master/docker/php-official/7.4) with partial nginx configuration from [webdevops/php-nginx:7.4](https://github.com/webdevops/Dockerfile/tree/master/docker/php-nginx/7.4).

**Original Dockerfiles updates:**
- Latest **nginx** version installed, `/index.php` routed to `/app/public/index.php`
- **Composer** installed
- **Xdebug** installed
- **mcedit** installed and configured to edit files via `edit` command using `modarin256` skin *(better compatibility using PHP Storm dark mode)*
- **Phalcon** extension preinstalled and does not need separate installation *(solves phalcon installation freezing using Docker Toolbox)*

**Latest release software versions:**

| Software | Version                                                          |
| -------- | ---------------------------------------------------------------- |
| PHP      | [7.4.*](https://www.php.net/releases/7_4_0.php)                  |
| Phalcon  | [4.0.6](https://github.com/phalcon/cphalcon/releases/tag/v4.0.6) |
| Nginx    | [latest stable](https://nginx.org/)                              |
| Xdebug   | [latest stable](https://xdebug.org/download)                     |
| Composer | [latest stable](https://getcomposer.org/download/)               |
