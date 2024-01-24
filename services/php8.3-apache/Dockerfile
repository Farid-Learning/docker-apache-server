FROM php:8.3-apache

ARG user
ARG uid

RUN apt-get update && apt-get install -y \
  git \
  curl \
  libpng-dev \
  libonig-dev \
  libxml2-dev \
  zip \
  unzip

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl pcmath gd

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -

RUN apt-get install -y nodejs

RUN curl -s https://getcomposer.org/installer | php

RUN mv composer.phar /usr/local/bin/composer

RUN useradd -G www-data,root -u $uid -d /home/$user $user

RUN mkdir -p /home/$user/.composer && \
  chown -R $user:$user /home/$user

COPY ./sites-available/*.conf /etc/apache2/sites-available/

RUN for site in /etc/apache2/sites-available/*.conf; do \
  a2ensite $(basename $site); \
  done

WORKDIR /var/www/html

USER $user

EXPOSE 80

CMD ["apache2-foreground"]
