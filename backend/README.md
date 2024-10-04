### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:VladimirAzanza/kittygram_final.git
```

```
cd backend/kittygram_backend
```

Cоздать и активировать виртуальное окружение:

```
python3.9 -m venv venv
```

* Если у вас Linux/macOS

    ```
    source venv/bin/activate
    ```

* Если у вас windows

    ```
    source venv/scripts/activate
    ```

```
python3 -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```
Создайте в корне проекта файл .env:

```
touch path_to_your_base_dir/.env
```
## Переменные среды

- `POSTGRES_DB` - имя базы данных
- `POSTGRES_USER` - пользователь базы данных
- `POSTGRES_PASSWORD` - пароль
- `DB_HOST` - имя хоста базы данных
- `DB_PORT` - порт базы данных 5432
- `SECRET_KEY` - секретный ключ Джанго
- `DEBUG` - логическое значение True or False (в разработке)
- `ALLOWED_HOSTS` - домен1 домен2 localhost 127.0.0.1
- `DB_ENGINE` - SQLite (в разработке) или PostgreSQL


Выполнить миграции:

```
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```