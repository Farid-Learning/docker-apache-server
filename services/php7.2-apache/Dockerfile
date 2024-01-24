FROM php:7.2-apache

COPY ./sites-available/*.conf /etc/apache2/sites-available/

RUN for site in /etc/apache2/sites-available/*.conf; do \
  a2ensite $(basename $site); \
  done

EXPOSE 80

CMD ["apache2-foreground"]