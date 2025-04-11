FROM php:8.2-apache

# Копируем конфиги Apache
COPY 000-default.conf /etc/apache2/sites-available/
COPY secondserver.conf /etc/apache2/sites-available/

# Включаем сайты
RUN a2ensite 000-default.conf && \
    a2ensite secondserver.conf && \
    a2enmod rewrite

# Копируем файлы
COPY html /var/www/html

# Настраиваем права
RUN useradd -u 1000 apacheuser && \
    chown -R apacheuser:apacheuser /var/www/html && \
    chmod -R 755 /var/www/html

USER apacheuser

EXPOSE 80
CMD ["apache2-foreground"]
