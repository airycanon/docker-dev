FROM php:7.1-fpm-alpine3.4

COPY repositories /etc/apk/repositories

ARG phpredis=3.1.4

RUN apk upgrade --update \
    && apk add libmcrypt-dev unzip libpng-dev freetype-dev libjpeg-turbo-dev postgresql-dev libbsd-dev \
    && docker-php-source extract \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$phpredis.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mv phpredis-$phpredis /usr/src/php/ext/redis \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd bcmath mcrypt pdo pdo_mysql pdo_pgsql redis zip iconv\
    && docker-php-source delete
