FROM php:8.0.1-fpm-alpine3.13

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS 1
ENV PHP_OPCACHE_MAX_ACCELERATED_FILES 7963
ENV PHP_OPCACHE_MEMORY_CONSUMPTION 192
ENV PHP_OPCACHE_MAX_WASTED_PERCENTAGE 10

COPY php.ini /usr/local/etc/php/
COPY opcache.ini /usr/local/etc/php/conf.d/

RUN apk upgrade --update && \
  apk --no-cache add --virtual build-dependencies \
  icu-dev \
  autoconf \
  make \
  g++ \
  gcc \
  oniguruma-dev \
  mariadb-dev \
  curl-dev \
  jpeg-dev \
  freetype \
  libpng \
  libjpeg-turbo \
  freetype-dev \
  libpng-dev \
  libjpeg-turbo-dev \
  libzip-dev \
  libxml2-dev \
  wget \
  unzip \
  git \
  exiftool

RUN docker-php-ext-configure gd \
  --with-freetype \
  --with-jpeg

RUN docker-php-ext-install -j$(nproc) \
  bcmath \
  gd \
  opcache \
  pdo_mysql \
  zip \
  intl \
  opcache \
  exif

RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
ENV COMPOSER_MEMORY_LIMIT -1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

RUN apk del --no-cache \
  autoconf \
  make \
  g++ \
  gcc \
  freetype-dev \
  libpng-dev \
  libjpeg-turbo-dev

WORKDIR /var/www
