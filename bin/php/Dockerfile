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
RUN apt install -y \
    vim git curl zip

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