# Лабораторная работа №8
1. Запустите контейнер и посотрите информацию о состоянии docker на хосте. Выведите информацию о типе операционной системы на которой установлен docker в файл, этом используйте командку docker info.
```
PS C:\Users\Eugene> docker info
Client:
 Version:    24.0.6
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.11.2-desktop.5
    Path:     C:\Program Files\Docker\cli-plugins\docker-buildx.exe
  compose: Docker Compose (Docker Inc.)
    Version:  v2.23.0-desktop.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-compose.exe
  dev: Docker Dev Environments (Docker Inc.)
    Version:  v0.1.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-dev.exe
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.20
    Path:     C:\Program Files\Docker\cli-plugins\docker-extension.exe
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v0.1.0-beta.9
    Path:     C:\Program Files\Docker\cli-plugins\docker-init.exe
  sbom: View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc.)
    Version:  0.6.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-sbom.exe
  scan: Docker Scan (Docker Inc.)
    Version:  v0.26.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-scan.exe
  scout: Docker Scout (Docker Inc.)
    Version:  v1.0.9
    Path:     C:\Program Files\Docker\cli-plugins\docker-scout.exe

Server:
 Containers: 8
  Running: 5
  Paused: 0
  Stopped: 3
 Images: 8
 Server Version: 24.0.6
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 8165feabfdfe38c65b599c4993d227328c231fca
 runc version: v1.1.8-0-g82f18fe
 init version: de40ad0
 Security Options:
  seccomp
   Profile: unconfined
 Kernel Version: 5.15.133.1-microsoft-standard-WSL2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 12
 Total Memory: 7.722GiB
 Name: DESKTOP-6JH1KPO
 ID: e1c02da5-d3d1-4977-96a4-7d929c4a83c5
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5555
  127.0.0.0/8
 Live Restore Enabled: false
```
2. Запустите произвольный контейнер. Выполните тестирование производительности в течении 3 минут. Оцените общую производительность во время выполения теста системы. Заморозьте контейнер. Разморозьте контейнер.
   ```
   docker run --rm jordi/ab -k -c 100 -n 1000 -t 180 http://host.docker.internal:80/
   docker pause my_apache_container
   docker unpause my_apache_container
   ```
3. Посотрите логи веб сервера apache, когда контейнер находится под тестированием производительности.
   ```
   docker logs my_apache_container
   ```
4. Запустите еще один контейнер с mongodb. Посмотрите статистику всех конетйнеров, используя (--format), не включая столбец PIDS. Запишите все результаты в файл.
   ```
    PS C:\Users\Eugene> docker stats --no-stream --format "table {{.Container}}\t{{.Name}}\t{{.CPUPerc}}\t{{.MemPerc}}\t{{.NetIO}}\t{{.BlockIO}}\t{{.MemUsage}}"
    CONTAINER      NAME                  CPU %     MEM %     NET I/O           BLOCK I/O   MEM USAGE / LIMIT
    0f9f811dce6e   mongodb2              0.21%     0.95%     726B / 0B         0B / 0B     74.9MiB / 7.722GiB
    30695d0b41bb   my_apache_container   0.00%     0.55%     9.31MB / 20.1MB   0B / 0B     43.63MiB / 7.722GiB
    85b2155ac748   app-flask-1           0.03%     0.33%     131kB / 45kB      0B / 0B     26.25MiB / 7.722GiB
    e928b43ecb77   app-mongodb-1         0.18%     2.38%     46.3kB / 130kB    0B / 0B     187.8MiB / 7.722GiB
   ```