FROM webdevops/php-nginx:7.4

ARG APP_ENV=production
ENV APP_ENV "$APP_ENV"
ENV fpm.pool.clear_env no
ENV fpm.pool.pm=ondemand
ENV fpm.pool.pm.max_children=50
ENV fpm.pool.pm.process_idle_timeout=10s
ENV fpm.pool.pm.max_requests=500
ENV COMPOSER_NO_INTERACTION 1

# Install apps and libs
RUN apt-get update && apt-get -y install \
    apt-utils \
    procps \
    mcedit \
    bsdtar \
    libaio1 \
    musl-dev \
    gettext \
    libpcre3-dev \
    gzip \
    git \
    software-properties-common

# Update and configure Nginx
COPY conf/nginx/10-location-root.conf /opt/docker/etc/nginx/vhost.common.d/10-location-root.conf
#COPY conf/nginx/nginx.list /etc/apt/sources.list.d/nginx.list
#RUN wget -qO - https://nginx.org/keys/nginx_signing.key | apt-key add - \
#    && apt-get update && apt-get remove nginx-common -y \
#    && echo '' | apt-get install nginx

# Configure `edit` dommand to use mcedit with `modarin256` skin
COPY conf/mcedit/mc.keymap /etc/mc/mc.keymap
COPY conf/mcedit/edit /usr/bin/edit
RUN chmod +x /usr/bin/edit

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

# Install Xdebug and PSR
RUN pecl install xdebug psr

# Configure Xdebug
COPY conf/xdebug/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Install Phalcon
COPY conf/phalcon/phalcon_4.0.5.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/phalcon.so

# Enable PSR, Phalcon and OPcache
RUN docker-php-ext-enable psr phalcon \
    && docker-php-ext-configure opcache --enable-opcache
