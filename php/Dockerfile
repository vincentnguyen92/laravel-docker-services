FROM php:7.4-fpm-alpine

# Install modules
RUN apk --update add --no-cache \
    autoconf \
    freetype-dev \
    libjpeg-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxml2-dev \
    libzip-dev \
    shadow && \
    apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing font-ipa && \
    docker-php-ext-install zip bcmath pdo pdo_mysql mysqli tokenizer xml pcntl opcache soap && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd && \
    apk add --no-cache $PHPIZE_DEPS && pecl install redis-5.1.1 && docker-php-ext-enable redis && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
    usermod -u 1000 www-data && groupmod -g 1000 www-data

# Setting PHP.ini
COPY ./custom.ini /usr/local/etc/php/conf.d/custom.ini

EXPOSE 9000
