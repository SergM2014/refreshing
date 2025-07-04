FROM php:8.4-fpm

# Install Composer
ENV COMPOSER_VERSION 2.8.9

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=$COMPOSER_VERSION

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_21.x | bash

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libssl-dev \
        libzip-dev \
        unzip \
        zip \
        nodejs \
    && apt-get clean \
    && docker-php-ext-configure gd \
    && docker-php-ext-configure zip \
    && docker-php-ext-install \
        gd \
        exif \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        pcntl \
        zip \
    && rm -rf /var/lib/apt/lists/*;

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug
# This needs in order to run xdebug from PhpStorm
ENV PHP_IDE_CONFIG 'serverName=DockerApp'

COPY ./docker/php/app.ini /usr/local/etc/php/conf.d/app.ini


WORKDIR /var/www/html

RUN chown -R www-data:www-data .
