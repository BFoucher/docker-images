FROM php:7.2-apache
ENV DEBIAN_FRONTEND=noninteractive
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update && apt-get install -y apt-utils

RUN apt-get install -y bash \
    libfreetype6-dev \
    libmcrypt-dev \
    zlib1g-dev \
    libicu-dev \
    g++ \
    apt-transport-https \
    zip \
    unzip \
    libxml2-dev \
    wget \
    vim \
    git \
    libmemcached-dev \
    libpq-dev \
    netcat \
    cron \
    mysql-common

RUN docker-php-ext-install -j$(nproc) iconv \
    bcmath \
    mbstring \
    pdo \
    pdo_mysql

RUN docker-php-ext-configure intl && docker-php-ext-install intl \
    zip \
    gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require "hirak/prestissimo:^0.3"
# Install NodeJS and npm package management
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -yq nodejs build-essential

# fix npm - not the latest version installed by apt-get
RUN npm install -g npm
RUN npm config set registry http://registry.npmjs.org/

# Install bower and gulp
RUN npm install -g bower gulp

RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN a2enmod rewrite ssl

ENV MYSQL_USER=admin \
    MYSQL_PASS=admin

RUN mkdir /app
WORKDIR /app

EXPOSE 80