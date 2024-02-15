FROM php:8.3-fpm-alpine3.19
#FROM php:8.3-fpm-bookworm
COPY php.ini /usr/local/etc/php/

# lib
RUN apk update \
 && apk add --no-cache --virtual build-dependencies gcc make autoconf libc-dev libtool \
 && apk add --no-cache --virtual zlib1g-dev libxml2-dev libzip-dev libpng-dev \
 && apk add --update --no-cache git openssh nodejs npm
#RUN apt-get update \
#  && apt-get install -y git nodejs npm libxml2-dev libzip-dev libpng-dev

# composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# php extension
RUN docker-php-ext-install xml pdo_mysql zip gd

# timezone
RUN apk add --update --no-cache --virtual build-dependencies tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    echo "Asia/Tokyo" > /etc/timezone && \
    apk del build-dependencies

WORKDIR /var/www

