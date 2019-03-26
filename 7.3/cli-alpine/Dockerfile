FROM php:7.3-cli-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

RUN apk --no-cache add shadow curl && \
    groupmod -g 101 www-data && \
    usermod -u 100 -g 101 www-data && \
    apk del shadow

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
        && mv composer.phar /usr/local/bin/ \
        && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

# Install PHP CodeSniffer
RUN composer global require "squizlabs/php_codesniffer=*"

# Install PHP CS Fixer
RUN composer global require friendsofphp/php-cs-fixer

# Install PHP Lint
RUN composer global require overtrue/phplint
