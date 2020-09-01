FROM php:7.4.7-fpm

WORKDIR /var/www/html

RUN mkdir -p /usr/local/etc/php-fpm.d/

#COPY php.ini /usr/local/etc/php/conf.d/php.ini

#COPY www.conf /usr/local/etc/php-fpm.d/www.conf
RUN rm /usr/local/etc/php-fpm.d/zz-docker.conf

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    default-mysql-client \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmagickwand-dev \
    libzip-dev \
    libonig-dev \
    locales \
    zip \
    unzip \
    jpegoptim optipng pngquant gifsicle \
    && pecl install imagick \
    && docker-php-ext-install pdo pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

RUN apt-get install -y zlib1g-dev && apt-get install -y libzip-dev
RUN docker-php-ext-install zip

RUN docker-php-ext-install gd

RUN composer global require laravel/installer
RUN ["/bin/bash", "-c", "echo PATH=$PATH:~/.composer/vendor/bin/ >> ~/.bashrc"]
RUN ["/bin/bash", "-c", "source ~/.bashrc"]

RUN apt-get install -y nodejs npm

RUN npm cache clean --force
RUN npm install -g n

RUN n 9.9.0

RUN ln -sf /usr/local/n/versions/node/9.9.0/bin/node /usr/bin/node

RUN npm install

RUN npm i -s -y cross-env

RUN chown -R www-data:www-data /var/www/html/
RUN chmod u+rwx,g+rx,o+rx /var/www/html/
RUN find /var/www/html/ -type d -exec chmod u+rwx,g+rx,o+rx {} +
RUN find /var/www/html/ -type f -exec chmod u+rw,g+rw,o+r {} +

CMD ["php-fpm", "--nodaemonize"]