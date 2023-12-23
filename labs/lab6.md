# Лабораторная работа №7
1. Создание простого приложения на Flask с подключением к MongoDB:
Создаем файл `app.py`:

```python
from flask import Flask
from pymongo import MongoClient
import os

app = Flask(__name__)

# Получаем значения переменных окружения для подключения к MongoDB
mongodb_host = os.environ.get('MONGODB_HOST')
mongodb_port = os.environ.get('MONGODB_PORT')

# Подключаемся к MongoDB
client = MongoClient(mongodb_host, int(mongodb_port))
db = client.test

@app.route('/')
def hello():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

2. Уменьшение размера образа:
Создаем  `Dockerfile`:

```Dockerfile
FROM python:3.9-slim-buster

WORKDIR /app

COPY app.py .

RUN pip install flask pymongo

CMD ["python", "app.py"]
```

3. Использование переменных окружения для подключения к БД:
Изменяем код в `app.py` следующим образом:

```python
mongodb_host = os.environ.get('MONGODB_HOST', 'localhost')
mongodb_port = os.environ.get('MONGODB_PORT', '27017')
```

4. Исключение root из Dockerfile: 
Изменения файл `Dockerfile`:

```Dockerfile
FROM python:3.9-slim-buster

RUN groupadd -r flaskgroup && useradd -r -g flaskgroup flaskuser

WORKDIR /app

COPY app.py .

RUN chown flaskuser:flaskgroup /app

USER flaskuser

RUN pip install flask pymongo

CMD ["python", "app.py"]
```

1. Проверка работоспособности сервисов:
Создаем файл `docker-compose.yml` со следующим содержимым:

```yaml
version: '3'
services:
  flask:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "5000:5000"
    environment:
      - MONGODB_HOST=mongodb
      - MONGODB_PORT=27017

  mongodb:
    image: mongo:4.4
```
Запускаем приложение с помощью команды `docker-compose up`.
