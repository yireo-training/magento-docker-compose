FROM php:8.2-fpm

ARG UNAME=www-data
ARG UGROUP=www-data
ARG UID=1000
ARG GID=1000
RUN usermod  --uid $UID $UNAME
RUN groupmod --gid $GID $UGROUP

#RUN useradd -G www-data jisse

RUN apt-get update && apt-get -y install \
    vim \
    cron \
    git \
    zlib1g-dev \
    zip \
    libzip-dev \
    redis-server \
    openssh-client \
    mariadb-client \
    apt-transport-https \
    git \
    zlib1g-dev \
    zip \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libsodium-dev \
    libicu-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev

RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install xsl
RUN docker-php-ext-install soap
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install sodium
RUN docker-php-ext-install zip
RUN docker-php-ext-install intl
RUN docker-php-ext-install sockets
RUN docker-php-ext-install opcache

RUN pecl install -o -f apcu && docker-php-ext-enable apcu
RUN pecl install -o -f xdebug && docker-php-ext-enable xdebug
RUN pecl install -o -f yaml && docker-php-ext-enable yaml
RUN pecl install -o -f redis &&  rm -rf /tmp/pear &&  docker-php-ext-enable redis

COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY general.ini /usr/local/etc/php/conf.d/general.ini

RUN curl -sOL https://getcomposer.org/download/2.0.13/composer.phar && mv composer.phar /usr/local/bin/composer && chmod 755 /usr/local/bin/composer && composer self-update
