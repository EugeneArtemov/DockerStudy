# Лабораторная работа №5
1. Повторите примеры для СУБД PostgeSQL, сгенерировав несколько произвольных таблиц.
    ```
    docker image pull postgres
    docker volume create pgdata
    docker run -d --name postgres-container -e POSTGRES_PASSWORD=mysecretpassword -v pgdata:/var/lib/postgresql/data postgres
    docker exec -it postgres-container psql -u postgres

    CREATE TABLE users (
       id SERIAL PRIMARY KEY,
       name VARCHAR(255),
       age INTEGER
   );

   INSERT INTO users (name, age) VALUES ('John', 25);
   INSERT INTO users (name, age) VALUES ('Maria', 30);
    ```
2. Проинспектируйте docker контейнер из примера 12, на наличие volume.
    ```
    "Volumes": {                                                                                                                                                   "/var/lib/postgresql/data": {}                                                                                                                         },      
    ```
3. Выполните пример 6 для nginx, предварительно узнав порт, скопируйте внутрь образа конфигурационный файл, а также измените стартовую страницу. Проверьте работоспособность испольщуя команду curl
   ```
   docker volume create --name storage
   docker container run -d -p 80:80 -v storage:/usr/share/nginx/html --name nginx-container nginx
   PS C:\Users\Eugene> Invoke-WebRequest -Uri http://localhost:8080


    StatusCode        : 200
    StatusDescription : OK
    Content           : <!DOCTYPE html>
                        <html>
                        <head>
                        <title>ÐÐ¾Ñ ÐºÐ°ÑÑÐ¾Ð¼Ð½Ð°Ñ ÑÑÑÐ°Ð½Ð¸ÑÐ°</title>
                        </head>
                        <body>
                        <h1>ÐÐ¾Ð±ÑÐ¾ Ð¿Ð¾Ð¶Ð°Ð»Ð¾Ð²Ð°ÑÑ Ð½Ð° Ð¼Ð¾Ñ ÐºÐ°ÑÑÐ¾Ð¼Ð½ÑÑ ÑÑÑÐ°Ð½Ð¸ÑÑ Nginx!<...
    RawContent        : HTTP/1.1 200 OK
                        Connection: keep-alive
                        Accept-Ranges: bytes
                        Content-Length: 281
                        Content-Type: text/html
                        Date: Fri, 22 Dec 2023 00:56:26 GMT
                        ETag: "655a71b5-119"
                        Last-Modified: Sun, 19 Nov 2023 ...
    Forms             : {}
    Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 281], [Content-Type, text/html]
                        ...}
    Images            : {}
    InputFields       : {}
    Links             : {}
    ParsedHtml        : mshtml.HTMLDocumentClass
    RawContentLength  : 281


   ```