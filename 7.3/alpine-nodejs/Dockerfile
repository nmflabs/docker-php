FROM nmflabs/php:7.3-cli-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

ARG NODE_VERSION=10.15.3

RUN apk update --no-cache && apk add --update --no-cache --virtual .build-deps \
        build-base \
        linux-headers \
        gnupg \
        git \
        python \
    && cd /tmp \
    && curl -sfSLO https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION.tar.gz | tar zxf - \
    && cd node-v$NODE_VERSION \
    && ./configure --prefix=/usr \
    && make -j1 && make install \
    && paxctl -cm /usr/bin/node \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --import && \
        curl -sfSLO https://yarnpkg.com/latest.tar.gz && \
        gpg --verify latest.tar.gz && \
        mkdir /usr/local/share/yarn && \
        tar -xf latest.tar.gz -C /usr/local/share/yarn --strip 1 && \
        ln -s /usr/local/share/yarn/bin/yarn /usr/local/bin/ && \
        ln -s /usr/local/share/yarn/bin/yarnpkg /usr/local/bin/ && \
        rm latest.tar.gz \
    && apk del .build-deps \
    && rm -rf \
        /tmp/* \
        /var/cache/apk/* \
        /root/.npm \
        /root/.node-gyp \
        /usr/lib/node_modules/npm/man \
        /usr/lib/node_modules/npm/doc \
        /usr/lib/node_modules/npm/html \
        /usr/share/man
