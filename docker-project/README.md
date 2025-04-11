# Docker-развертывание Nginx + Apache

## Образы на Docker Hub
- Nginx: `docker pull yourusername/my-nginx:v1`
- Apache: `docker pull yourusername/my-apache:v1`

## Запуск
```bash
docker run -d --name nginx-container -p 8083:80 yourusername/my-nginx:v1
docker run -d --name apache-container -p 8081:80 yourusername/my-apache:v1
