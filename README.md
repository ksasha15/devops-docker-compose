# devops-docker-compose

#### Описание выполнения задания:
- Завести репозиторий в Docker Hub.
- Упаковать микросервисное приложение в Dockerfile
- Собрать образ из полученного Dockerfile
- Запушить в репозиторий образы из предыдущего шага.
- Настроить хранение данных приложения/бд в volume.
- Создать отдельную Docker-network для стэка приложения.
- Запустить приложение в контейнерах в Yandex Cloud.
Предоставить доступ к ВМ, для проверки доступности образов.

#### Репозиторий в Докер Хабе:
https://hub.docker.com/repository/docker/ksasha15/compose/general

#### Описание микросервисов
Основа взята из описания на Docker Docs. Все файлы проекта находятся в этом репозитории. Сервис считает количество обращений к сайту. Все настройки приложения, порты, сети, подключаемые тома согласно compose.yaml. Ниже привожу код работы:
```
root@Ubuntu22:/home/u24/Compose# ll
total 36
drwxrwxr-x  3 u24  u24  4096 Apr  5 10:34 ./
drwxr-x--- 23 u24  u24  4096 Apr  5 06:40 ../
-rw-rw-r--  1 u24  u24   321 Apr  5 08:05 app.py
-rw-rw-r--  1 u24  u24   718 Apr  5 09:52 compose.yaml
-rw-rw-r--  1 u24  u24   256 Apr  5 07:02 Dockerfile
-rw-rw-r--  1 u24  u24    34 Apr  5 06:38 .dockerignore
-rw-rw-r--  1 u24  u24    47 Apr  5 06:34 .env
drwxr-xr-x  8 root root 4096 Apr  5 10:40 .git/
-rw-rw-r--  1 u24  u24    12 Apr  5 07:49 requirements.txt
root@Ubuntu22:/home/u24/Compose# docker compose up -d
[+] up 3/3
 ✔ Network compose_app_network Created                                       0.2s
 ✔ Container compose-redis-1   Healthy                                       6.1s
 ✔ Container compose-web-1     Started                                       6.5s
root@Ubuntu22:/home/u24/Compose# curl localhost:8000
Hello from Compose Watch!! I have been seen 1 time(s).
root@Ubuntu22:/home/u24/Compose# curl localhost:8000
Hello from Compose Watch!! I have been seen 2 time(s).
root@Ubuntu22:/home/u24/Compose# curl localhost:8000
Hello from Compose Watch!! I have been seen 3 time(s).
root@Ubuntu22:/home/u24/Compose#
```
#### Доступ на YandexCloud
