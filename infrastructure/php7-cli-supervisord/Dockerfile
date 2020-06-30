# See https://github.com/docker-library/php/blob/master/7.4/cli/Dockerfile
FROM php:7.4-cli
ARG TIMEZONE


RUN apt-get update && apt-get install -y \
    openssl \
    git \
    supervisor \
    unzip

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

#Install AMPQ
RUN apt-get install -y \
librabbitmq-dev \
libssh-dev \
&& pecl install amqp \
&& docker-php-ext-enable amqp

# Install PHP Redis extension
RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN echo 'alias sf="php app/console"' >> ~/.bashrc \
&& echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/symfony
