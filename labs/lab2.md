# Лабораторная работа №3
1. Установите докер registry
    ```
    docker run -d -p 5000:5000 --restart=always --name registry registry:2
    ```
2. Установите лимит на контейнер apache
    ```
    docker run -d --name my-apache-container -p 8080:80 --memory 512m httpd:latest

    docker stats
    CONTAINER ID   NAME                  CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O   PIDS
    6b90b716f5a8   my-apache-container   0.00%     41.52MiB / 512MiB     8.11%     3.84kB / 2.27kB   0B / 0B     109
    d506416e172a   registry              0.00%     15.02MiB / 7.722GiB   0.19%     2.8kB / 1.01kB    0B / 0B     10
    ```
    