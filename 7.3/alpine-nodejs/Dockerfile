FROM nmflabs/php:7.3-cli-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

ARG NODE_VERSION=10.15.3

RUN apk -U add curl \
        git \
        make \
        gcc \
        g++ \
        python \
        linux-headers \
        paxctl \
        libgcc \
        libstdc++ \
        binutils-gold \
        ca-certificates \
    && cd /tmp \
    && curl --silent --ssl https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION.tar.gz | tar zxf - \
    && cd node-v$NODE_VERSION \
    && ./configure --prefix=/usr \
    && make -j1 && make install \
    && paxctl -cm /usr/bin/node \
    && apk del \
        curl \
        git \
        make \
        gcc \
        g++ \
        python \
        linux-headers \
        paxctl \
        grep \
        binutils-gold \
        ca-certificates \
    && rm -rf \
        /tmp/* \
        /var/cache/apk/* \
        /root/.npm \
        /root/.node-gyp \
        /usr/lib/node_modules/npm/man \
        /usr/lib/node_modules/npm/doc \
        /usr/lib/node_modules/npm/html \
        /usr/share/man
    && apk -U add yarn

CMD ["/bin/bash"]
