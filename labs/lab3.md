# Лабораторная работа №4
1. Создайте одностраничный сайт(используйте любой стек технологий).
    Предварительно в директории 'C:\Users\Eugene\Documents\Doc' были добавлены Dockerfiles и index.html, созданные на подобии практической части лабораторной работы.
2.  Создайте для него Dockerfile, запустите.
    ```
    C:\Users\Eugene\Documents\Doc> docker build . -t localhost:5000/nginx:0.0.1
    C:\Users\Eugene\Documents\Doc> docker run -itd -p 8011:80 --name nginx-dock localhost:5000/nginx:0.0.1
    PS C:\Users\Eugene\Documents\Doc> docker logs nginx-dock
    /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
    /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
    10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
    10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
    /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
    /docker-entrypoint.sh: Configuration complete; ready for start up
    2023/12/21 14:48:31 [notice] 1#1: using the "epoll" event method
    2023/12/21 14:48:31 [notice] 1#1: nginx/1.25.3
    2023/12/21 14:48:31 [notice] 1#1: built by gcc 12.2.1 20220924 (Alpine 12.2.1_git20220924-r10)
    2023/12/21 14:48:31 [notice] 1#1: OS: Linux 5.15.133.1-microsoft-standard-WSL2
    2023/12/21 14:48:31 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
    2023/12/21 14:48:31 [notice] 1#1: start worker processes
    2023/12/21 14:48:31 [notice] 1#1: start worker process 30
    2023/12/21 14:48:31 [notice] 1#1: start worker process 31
    ...
    PS C:\Users\Eugene\Documents\Doc> docker images
    REPOSITORY             TAG           IMAGE ID       CREATED         SIZE
    localhost:5000/nginx   0.0.1         aaee94701c2c   5 minutes ago   42.6MB
    ```