FROM php:7.1-fpm-alpine

ARG user
ARG uid

RUN apk add --update --no-cache icu-libs \
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
        npm  \
        doas

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
    echo permit persist :$user > /etc/doas.conf

RUN pecl install xdebug-2.9.8 \
    && docker-php-ext-enable xdebug

# Clean cache
RUN rm -rf /var/cache/apk/* && docker-php-source delete

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user

COPY docker_files/php/conf.d/php.ini /usr/local/etc/php/php.ini
COPY docker_files/php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN mkdir /etc/supervisor
COPY docker_files/supervisor/supervisor.conf /etc/supervisor/supervisor.conf
COPY docker_files/supervisor/conf.d /etc/supervisor/conf.d

WORKDIR /var/www/

CMD ["/usr/bin/supervisord","-c","/etc/supervisor/supervisor.conf"]

USER $user
