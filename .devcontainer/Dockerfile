FROM dunglas/frankenphp

# Create a non-root user and set permissions
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=

# add additional extensions here:
RUN install-php-extensions \
    pdo_mysql \
    pdo_pgsql \
    gd \
    intl \
    zip \
    xdebug \
    opcache

#install composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm -rf composer-setup.php

# Add user and group, and set permissions for required folders
RUN groupadd --gid   \
    && useradd -s /bin/bash --uid  --gid  -m  \
    && chown -R : /app

# Grant additional capabilities if needed
RUN setcap CAP_NET_BIND_SERVICE=+eip /usr/local/bin/frankenphp \
    && chown -R : /data/caddy /config/caddy

# Switch to the non-root user
USER 

# Changing Workdir
WORKDIR /app
