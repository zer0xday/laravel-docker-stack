FROM php:7.4.8-fpm

# Use non interactive mode to prevent TUI popups
ENV DEBIAN_FRONTEND noninteractive

# Args
ARG NODEJS_VERSION=14.x

# Update & upgrade
RUN apt-get -y update --fix-missing && \
    apt-get upgrade -y && \
    apt-get --no-install-recommends install -y apt-utils

# Install tools
RUN apt-get install -y \
    vim git curl zip

# Install important libs
RUN apt-get install -y \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    libonig-dev

# Install important php extensions
RUN set -eux; \
    # Install the PHP pdo_mysql extention
    docker-php-ext-install pdo_mysql; \
    # Install the PHP gd library
    docker-php-ext-configure gd \
            --prefix=/usr \
            --with-jpeg \
            --with-freetype; \
    docker-php-ext-install gd

# Install xdebug
RUN pecl install xdebug-2.9.8 && \
    docker-php-ext-enable xdebug

# Instal composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# nodejs & npm
# get install script and pass it to execute:
RUN curl -sL https://deb.nodesource.com/setup_$NODEJS_VERSION | bash
# and install node
RUN apt-get -y install nodejs

# Clean-up
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /myapp/

RUN useradd -g www-data user
USER user