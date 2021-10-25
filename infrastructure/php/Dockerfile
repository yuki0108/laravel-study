FROM php:7.4-fpm-alpine

ARG PSYSH_DIR=/usr/local/share/psysh
ARG PHP_MANUAL_URL=http://psysh.org/manual/ja/php_manual.sqlite

WORKDIR /var/www/app

ARG TZ=Asia/Tokyo


RUN set -eux && \
    apk update && \
    apk add --update --no-cache oniguruma-dev && \
    apk add --update --no-cache --virtual=.build-dependencies \
        autoconf \
        gcc \
        g++ \
        make \
        tzdata && \
    apk add --update --no-cache \
        icu-dev \
        libzip-dev && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    echo ${TZ} > /etc/timezone && \
    pecl install xdebug && \
    apk del .build-dependencies && \
    docker-php-ext-install intl pdo_mysql mbstring zip bcmath && \
    docker-php-ext-enable xdebug && \
    mkdir $PSYSH_DIR && wget $PHP_MANUAL_URL -P $PSYSH_DIR

COPY ./infrastructure/php/php.ini /usr/local/etc/php

COPY --from=composer:2.1 /usr/bin/composer /usr/bin/composer

RUN composer config -g process-timeout 3600 && \
    composer config -g repos.packagist composer https://packagist.org