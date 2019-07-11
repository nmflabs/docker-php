FROM nmflabs/php:7.3-cli-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

ARG TZ=Asia/Jakarta
ENV TZ ${TZ}

RUN apk update --no-cache && apk add --no-cache --virtual .build-deps \
    build-base \
    autoconf \
    zlib-dev \
    libxml2-dev

RUN apk add --no-cache \
        git \
        zip \
        libzip-dev \
        libjpeg-turbo-dev \
        freetype-dev \
        libpng-dev \
        imagemagick-dev \
        jpegoptim \
        optipng \
        pngquant \
        gifsicle \
    \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    \
    && docker-php-ext-configure \
        zip --with-libzip \
    \
    && docker-php-ext-configure \
        gd --with-gd \
            --with-jpeg-dir=/usr/include \
            --with-png-dir=/usr/include \
            --with-freetype-dir=/usr/include \
    \
    && docker-php-ext-install \
        zip \
        pdo \
        bcmath \
        pdo_mysql \
        exif \
        mysqli \
        mbstring \
        pcntl \
        dom \
        gd \
    \
    && pecl install -o -f \
        redis \
        imagick \
    \
    && docker-php-ext-enable \
        redis \
        imagick \
    \
    && apk del --no-network .build-deps \
    && rm -rf /var/cache/apk/*
