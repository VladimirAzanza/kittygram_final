# Настроить запуск проекта Kittygram в контейнерах и CI/CD с помощью GitHub Actions

Kittygram - социальная сеть для обмена фотографиями любимых питомцев.

## Инструкция по настройке проекта

- Клонировать репозиторий локально:
```
git clone git@github.com:VladimirAzanza/kittygram_final.git
cd kittygram_final
```
- Настройте Dockerfile backend/frontend в соответсвии с вашими потребностями (Можете оставить настройки по умолчанию):
```
nano backend/Dockerfile
nano frontend/Dockerfile
```
- Настройте "gateway" в соответствии с вашими потребностями для конфигурации Nginx (Можете оставить настройки по умолчанию):
```
nano nginx/Dockerfile
nano nginx/nginx.conf
```
- Настройте оркестрации контейнеры в соответствии с вашими потребностями (Можете оставить настройки по умолчанию):
```
nano docker-compose.production.yml
```
- Установите Docker на сервере:
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```
- Создайте на сервере директорию kittygram:
```
mkdir kittygram
```
- Создайте в файл .env:

```
cd kittygram
touch .env
```
- Переменные среды
```
- `POSTGRES_DB` - имя базы данных
- `POSTGRES_USER` - пользователь базы данных
- `POSTGRES_PASSWORD` - пароль
- `DB_HOST` - имя хоста базы данных
- `DB_PORT` - порт базы данных 5432
- `SECRET_KEY` - секретный ключ Джанго
- `DEBUG` - логическое значение True or False (в разработке)
- `ALLOWED_HOSTS` - домен1 домен2 localhost 127.0.0.1
- `DB_ENGINE` - SQLite (в разработке) или PostgreSQL
```
- Автоматизируйте CI/CD с помощью GitHub Actions (Можете оставить настройки по умолчанию):
```
nano .github/workflows/main.yml
```
- Добавьте секреты в GitHub Actions:
```
   DOCKER_USERNAME 
   DOCKER_PASSWORD
   HOST - Адрес IP
   USER - имя пользователя на сервере
   SSH_KEY
   SSH_PASSPHRASE
   TELEGRAM_TO - ID телеграм-аккаунта
   TELEGRAM_TOKEN - токен бота, можно его получить через @BotFather 
```

## Настройте Nginx на сервере для прослушивания правильного порта: по умолчанию используется порт 9000

```
sudo nano /etc/nginx/sites-enabled/default
```

```
server {
    server_name <Ваш домен>;

    location / {
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:9000;
    }
}
```
### Проверьте правильность конфигурации Nginx:

```
sudo nginx -t
```

### Перезапустите Nginx:
```
sudo service nginx reload
```

### Стек

Python 3.9
Django 3.2.3
Django Rest Framework 3.12.4
Gunicorn 20.1.0
Docker 27.3.1
PostgreSQL 13


