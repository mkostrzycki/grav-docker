FROM php:8.3-fpm-alpine

RUN apk update --no-cache && \
    apk upgrade --no-cache

RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    linux-headers
RUN apk add --no-cache \
    freetype-dev \
    jpeg-dev \
    libzip-dev

RUN pecl install APCu && \
    docker-php-ext-enable apcu

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg
RUN docker-php-ext-install gd

RUN docker-php-ext-enable opcache

RUN docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#COPY php.ini $PHP_INI_DIR

RUN apk del --no-network .build-deps
RUN rm -rf /tmp/* /var/tmp/*
