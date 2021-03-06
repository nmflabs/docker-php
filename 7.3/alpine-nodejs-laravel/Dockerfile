FROM nmflabs/php:7.3-cli-alpine-laravel

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

ENV NODE_VERSION 10.15.3
ENV YARN_VERSION 1.13.0

# Based on https://github.com/nodejs/docker-node/blob/master/10/alpine/Dockerfile

RUN addgroup -g 1000 node \
    && adduser -u 1000 -G node -s /bin/sh -D node \
    && apk add --update --no-cache --virtual .build-deps \
        build-base \
        linux-headers \
        gnupg \
        python \
    && apk add --update --no-cache \
        # Need some tools to make node_modules dependencies work.
        # Native Module need below, the first one.
        make gcc g++ python \
        zlib-dev \
        libc6-compat \
        libjpeg-turbo-dev \
        libpng-dev \
    && for key in \
        # NodeJs
        94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
        FD3A5288F042B6850C66B31F09FE44734EB7990E \
        71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
        DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
        C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
        B9AE9905FFD7803F25714661B63B535A4C206CA9 \
        77984A986EBC2AA786BC0F66B01FBB92821C587A \
        8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 \
        4ED778F539E3634C779C87C6D7062848A1AB005C \
        A48C2BEE680E841632CD4E44F07496B3EB3C1762 \
        B9E2F5981AA6E0CD28160D9FF13993A75599653C \
        # Yarn
        6A010C5166006599AA17F08146C2130DFD2497F5 \
    ; do \
        gpg --batch --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys "$key" || \
        gpg --batch --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys "$key" || \
        gpg --batch --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" ; \
    done \
    # Installing NodeJS
        && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION.tar.xz" \
        && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
        && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
        && grep " node-v$NODE_VERSION.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
        && tar -xf "node-v$NODE_VERSION.tar.xz" \
        && cd "node-v$NODE_VERSION" \
        && ./configure \
        && make -j$(getconf _NPROCESSORS_ONLN) \
        && make install \
        && cd .. \
        && rm -Rf "node-v$NODE_VERSION" \
        && rm "node-v$NODE_VERSION.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
    # Installing Yarn
        && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
        && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz.asc" \
        && gpg --batch --verify yarn-v$YARN_VERSION.tar.gz.asc yarn-v$YARN_VERSION.tar.gz \
        && mkdir -p /opt \
        && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
        && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
        && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
        && rm yarn-v$YARN_VERSION.tar.gz.asc yarn-v$YARN_VERSION.tar.gz \
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

CMD ["/bin/bash"]
