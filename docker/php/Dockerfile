FROM nginx:alpine
EXPOSE 80 443

FROM php:7.4-fpm-alpine

RUN echo 'http://dl-4.alpinelinux.org/alpine/edge/community/' >> /etc/apk/repositories

RUN apk update \
    && apk add \
        --no-cache $PHPIZE_DEPS \
        python3 \
        py-pip \
        libwebp-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libsodium \
        libzip-dev \
        nodejs \
        npm \
        postgresql-dev \
        unzip \
        zip \
    && pecl install redis \
    && rm -rf /tmp/pear \
    && pip install supervisor

RUN docker-php-ext-enable redis
RUN docker-php-ext-install bcmath \
    ctype \
    fileinfo \
    gd \
    json \
    mysqli \
    pcntl \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    tokenizer \
    zip

RUN curl --silent --show-error https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

CMD ["php-fpm"]
