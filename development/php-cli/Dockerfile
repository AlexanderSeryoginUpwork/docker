FROM php:7.4-cli

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis


RUN apt-get update && apt-get install -y libpq-dev unzip libzip-dev mariadb-client \
    && docker-php-ext-install pdo_mysql zip
#    && pecl install xdebug-2.7.2
#    && docker-php-ext-enable xdebug

#COPY ./docker/development/php-cli/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/bin --filename=composer --quiet

ENV COMPOSER_ALLOW_SUPERUSER 1

WORKDIR /var/www/html
