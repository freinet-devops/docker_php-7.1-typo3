FROM php:7.1-fpm-alpine
# compared to
# Install gd

LABEL summary="php-7.1 with extensions and external programs for typo3" \
      version="php7.1-fpm-alpine" \
      name="freinet/typo3-sshd" \
      maintainer="Sebastian Pitsch <pitsch@freinet.de>"

USER root

RUN apk -u add --no-cache freetype libjpeg-turbo libpng icu-libs zlib bash composer graphicsmagick
RUN apk add --no-cache freetype-dev libpng-dev libjpeg-turbo-dev zlib-dev icu-dev \
    && docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure intl \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) intl \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev zlib-dev icu-dev

EXPOSE 9000