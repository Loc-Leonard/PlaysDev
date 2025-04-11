FROM httpd:alpine

# Копируем основную конфигурацию
COPY httpd.conf /usr/local/apache2/conf/httpd.conf

# Копируем дополнительные конфиги
COPY sites/ /usr/local/apache2/conf/extra/

# Создаем пользователя и устанавливаем права
RUN adduser -D -u 1000 apacheuser && \
    chown -R apacheuser:apacheuser /usr/local/apache2 && \
    chmod -R 755 /usr/local/apache2/htdocs

USER apacheuser

EXPOSE 80

CMD ["httpd-foreground"]
