FROM php:8.2-fpm-alpine

ARG user
ARG uid

RUN apk add --update --no-cache icu-libs \
        doas \
        libintl \
        build-base \
        zlib-dev \
        cyrus-sasl-dev \
        libgsasl-dev \
        oniguruma-dev \
        procps \
        imagemagick \
        patch \
        bash \
        htop \
        acl \
        apk-cron \
        augeas-dev \
        autoconf \
        curl \
        ca-certificates \
        dialog \
        freetype-dev \
        gomplate \
        git \
        gcc \
        gettext-dev \
        icu-dev \
        libcurl \
        libffi-dev \
        libgcrypt-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libmcrypt-dev \
        libressl-dev \
        libxslt-dev \
        libzip-dev \
        linux-headers \
        libxml2-dev \
        ldb-dev \
        make \
        musl-dev \
        mysql-client \
        openssh-client \
        pcre-dev \
        ssmtp \
        sqlite-dev \
        supervisor \
        su-exec \
        wget \
        nodejs \
        npm

RUN docker-php-ext-install exif \
        mysqli \
        opcache \
        xsl \
        bcmath \
        gd \
        gettext \
        intl \
        opcache \
        pcntl \
        soap \
        zip \
        calendar \
        pdo_mysql \
        pdo

RUN adduser -u $uid $user; \
    echo $user:bktl57m | chpasswd; \
    echo permit $user as root > /etc/doas.d/doas.conf

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Clean
RUN rm -rf /var/cache/apk/* && docker-php-source delete

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user

WORKDIR /var/www/

USER $user