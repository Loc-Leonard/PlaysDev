# Этап сборки (для генерации SSL при необходимости)
FROM nginx:alpine AS builder

# Установка openssl для генерации сертификатов
RUN apk add --no-cache openssl

# Генерация self-signed сертификата (если нет своих)
RUN mkdir -p /etc/nginx/ssl && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/nginx/ssl/key.pem \
    -out /etc/nginx/ssl/cert.pem \
    -subj "/CN=localhost"

# Основной этап
FROM nginx:alpine

# Копируем SSL сертификаты (если есть свои - замените)
COPY --from=builder /etc/nginx/ssl /etc/nginx/ssl

# Копируем конфигурации
COPY nginx.conf /etc/nginx/nginx.conf
COPY sites-enabled/ /etc/nginx/conf.d/

# Создаем не-root пользователя
RUN adduser -D -u 1000 nginxuser && \
    chown -R nginxuser:nginxuser /var/cache/nginx && \
    chown -R nginxuser:nginxuser /usr/share/nginx/html

# Права для SSL сертификатов
RUN chmod 644 /etc/nginx/ssl/cert.pem && \
    chmod 600 /etc/nginx/ssl/key.pem

USER nginxuser

EXPOSE 443

CMD ["nginx", "-g", "daemon off;"]
