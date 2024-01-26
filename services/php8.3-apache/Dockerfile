# Usamos la imagen oficial de PHP 8.3 con Apache
FROM php:8.3-apache

# Actualizamos e instalamos dependencias necesarias
RUN apt-get update && apt-get install -y \
  libpng-dev \
  libjpeg-dev \
  libfreetype6-dev \
  zip \
  unzip \
  git \
  ctype \
  json \
  mbstring \
  openssl \
  pdo \
  tokenizer \
  xml \
  intl \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Instalamos Composer globalmente
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -

RUN apt-get install -y nodejs

# Copiamos el archivo de configuración de Apache para habilitar reescritura de URL
COPY ./sites-available/*.conf /etc/apache2/sites-available/

RUN for site in /etc/apache2/sites-available/*.conf; do \
  a2ensite $(basename $site); \
  done

# Exponemos el puerto 80 para acceder al servidor web
EXPOSE 80

# Ejecutamos Apache en primer plano al iniciar el contenedor
CMD ["apache2-foreground"]
