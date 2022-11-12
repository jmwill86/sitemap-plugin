FROM php:8-fpm-alpine

RUN apk update
RUN apk add --no-cache $PHPIZE_DEPS \
    exiftool \
    zip \
    libzip \
    zlib-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    git 

RUN docker-php-ext-install exif gd

ADD /php.ini /usr/local/etc/php/

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

# Final vars
WORKDIR /usr/src
EXPOSE 9000 80 443
CMD ["php-fpm", "--nodaemonize"]