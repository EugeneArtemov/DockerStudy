# Лабораторная работа №2
1. Создание и запуск контейнера "mydoc".

```
PS C:\Users\Eugene> docker run -itd -p 8099:80 --name mydoc nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
578acb154839: Pull complete
e398db710407: Pull complete
85c41ebe6d66: Pull complete
7170a263b582: Pull complete
8f28d06e2e2e: Pull complete
6f837de2f887: Pull complete
c1dfc7e1671e: Pull complete
Digest: sha256:86e53c4c16a6a276b204b0fd3a8143d86547c967dc8258b3d47c3a21bb68d3c6
Status: Downloaded newer image for nginx:latest
8ee97b876235651114836c3d646d46d0aad9652f5e7d17f6837b61532b729f65 
```

2. Проверка состояния контейнера. Из текста консоли понятно, что контейнер "mydoc" был успешно создан и запущен, так же мы видим неактивный контейнер, созданный для теста с помощью графического интерфейса программы "Docker Dekstop" до этого.

```
PS C:\Users\Eugene> docker container ls -a -s
CONTAINER ID   IMAGE                             COMMAND                  CREATED          STATUS                    PORTS                  NAMES               SIZE
8ee97b876235   nginx                             "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes             0.0.0.0:8099->80/tcp   mydoc               1.09kB (virtual 187MB)
298b16b8860d   docker/welcome-to-docker:latest   "/docker-entrypoint.…"   29 hours ago     Exited (0) 24 hours ago                          welcome-to-docker   1.09kB (virtual 18.6MB)
```

3. Изменил стартовую html страницу произвольным образом для образа веб-сервера nginx.
```
PS C:\Users\Eugene> docker exec -it mydoc bash
root@8ee97b876235:/usr/share/nginx/html# vi index.html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>POMENYAL</h1>

</body>
</html>
```

Изменил стартовую html страницу произвольным образом для образа веб-сервера apache.
    
```
PS C:\Users\Eugene> docker run -d --name my-apache-container -p 8080:80 httpd:latest
Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
578acb154839: Already exists
c1a8c8567b78: Pull complete
10b9ab03bf45: Pull complete
74dbedf7ddc0: Pull complete
6a3b76b70f73: Pull complete
Digest: sha256:4e24356b4b0aa7a961e7dfb9e1e5025ca3874c532fa5d999f13f8fc33c09d1b7
Status: Downloaded newer image for httpd:latest
17c471573b3a8c2824993cc8668d7b288c0da2918574f7be672d67290e40c6c8
PS C:\Users\Eugene> docker exec -it my-apache-container bash
root@17c471573b3a:/usr/local/apache2# /usr/local/apache2/conf
bash: /usr/local/apache2/conf: Is a directory
root@17c471573b3a:/usr/local/apache2# vim httpd.conf
```    
