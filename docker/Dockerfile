FROM php:7.4-fpm

ARG USER=user
ARG UID=1000
ARG PORT=9000
ARG WORKDIR=/var/www


EXPOSE $PORT

RUN apt-get update && apt-get install -y \
    libzip-dev \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    wget \
    openssl \
    libssl-dev \
    nano \
    git \
    --fix-missing && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install \
    zip \
    pdo_mysql \
    mbstring \
    exif \
    pcntl \
    bcmath \
    gd \
    soap

RUN pecl install \
    xdebug-3.0.3 \
    mailparse \
    redis && \
    docker-php-ext-enable \
    xdebug \
    mailparse \
    redis

COPY --from=composer:2.8.4 /usr/bin/composer /usr/bin/composer

RUN useradd -G www-data,root -u $UID -d /home/$USER $USER && \
    mkdir -p /home/$USER/.composer && \
    chown -R $USER:$USER /home/$US

#RUN chown -R www-data:www-data /var/www/html \
#    && chmod -R 755 /var/www/html/storage \
#    && chmod -R 755 /var/www/html/bootstrap/cache

WORKDIR $WORKDIR

USER $USER

#COPY ./php.ini /usr/local/etc/php/php.ini
