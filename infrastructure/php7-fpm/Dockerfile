# See https://github.com/docker-library/php/blob/master/7.4/fpm/Dockerfile
FROM php:7.4-fpm
ARG TIMEZONE


RUN apt-get update && apt-get install -y \
    openssl \
    git \
    unzip \
    #Rabbit MQ
    librabbitmq-dev \
    libssh-dev
    #End Rabbit MQ


# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
&& composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
&& printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
&& "date"

ADD conf.d/php.ini /usr/local/etc/php/conf.d/php.ini

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql

#OpCache
RUN docker-php-ext-install opcache
ADD conf.d/opcache.ini /usr/local/etc/php/conf.d/opcache.ini


# install xdebug
RUN pecl install xdebug \
&& docker-php-ext-enable xdebug
ADD conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

#Install AMPQ
RUN pecl install amqp \
&& docker-php-ext-enable amqp

# Install PHP Redis extension
RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN echo 'alias sf="php app/console"' >> ~/.bashrc \
&& echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/symfony
