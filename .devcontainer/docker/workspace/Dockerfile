FROM php:8.1.17-fpm-alpine3.17

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

ARG TIME_ZONE

RUN apk update \
    && apk add git postgresql-client libzip-dev libjpeg-turbo-dev libpng-dev freetype-dev nodejs npm \
    && apk add --no-cache --virtual .build-dependencies autoconf gcc g++ make postgresql-dev linux-headers tzdata \
    && docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd pdo_pgsql zip bcmath \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && cp /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
    && apk del --no-network .build-dependencies

EXPOSE 5173