FROM php:7.3-cli-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

RUN apk --no-cache add bash openssh \
    \
    # Install Composer
    && curl -sS https://getcomposer.org/installer | php \
        && mv composer.phar /usr/local/bin/ \
        && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer \
    \
    # Install PHP CodeSniffer
    && composer global require "squizlabs/php_codesniffer=*" \
    \
    # Install PHP CS Fixer
    && composer global require friendsofphp/php-cs-fixer \
    \
    # Install PHP Lint
    && composer global require overtrue/phplint

ENV PATH="~/.composer/vendor/bin:${PATH}"

CMD ["/bin/bash"]
