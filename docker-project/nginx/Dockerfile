FROM nginx:alpine

# Удаляем дефолтный конфиг
RUN rm /etc/nginx/conf.d/default.conf

# Копируем наши конфиги
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/

# Копируем статику (HTML, картинки, музыку)
COPY html /var/www/html

# Права для статики
RUN chown -R nginx:nginx /var/www/html && \
    chmod -R 755 /var/www/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
