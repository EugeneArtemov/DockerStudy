# Лабораторная работа №8
1. Создайте временный контейнер, который монтирует нужный Docker Volume и другой том для сохранения резервной копии. Например:
   ```
    bash docker run --rm -v resrv:/backup -v tom:/data alpine tar -czvf /backup/backup.tar.gz /data
   ```
2. Чтобы восстановить резервную копию, выполните следующие действия:
   ```
   bash docker run --rm -v resrv:/backup -v tom2:/data alpine tar -xzvf /backup/backup.tar.gz -C /data
   ```
