# otus_9
Docker

*Задание:*
* 1 *Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx). Собранный образ необходимо запушить в dockerhub и дать ссылку на ваш репозиторий.*
* 2 *Определите разницу между контейнером и образом*
* 3 *Можно ли в контейнере собрать ядро?*

# кастомный образ nginx на базе alpine

Мой образ на докерхабе
https://hub.docker.com/repository/docker/edo2681/nginx-alpine
```
docker pull edo2681/nginx-alpine
docker run --name nginx-alpine -dp 82:80 edo2681/nginx-alpine
```

пишу для себя, потому что потом забуду.
* установка docker на centos 7
Обновить локальную базу пакетов:
```
sudo yum check-update
```
Добавим репозиторий, загрузим последнюю версию ПО и установит его:
```
curl -fsSL https://get.docker.com/ | sh
```
Чтобы запускать докер не от имени пользователя root добавим пользователя в созданную после установки группу docker:
```
sudo usermod -aG docker $USER
```
Запустим демон Docker после окончания установки:
```
sudo systemctl start docker
```
Чтобы проверить, что команды выполняются от имени текущего пользователя - Log out / log back
```
docker run hello-world
```
![Image alt](https://github.com/Edo1993/otus_9/raw/master/12.png)

Убедиться в том, что демон стартовал без ошибок и предупреждений:
```
sudo systemctl status docker
```
В результате должно появиться подобное сообщение:
![Image alt](https://github.com/Edo1993/otus_9/raw/master/11.png)

Dockerfile, html запилили, посмотреть, что локально работает.
Сборка в текущей директории. 
```
docker build -t <имя> .
```
Запустить контейнер 
```
docker run -d -p 82:80 container_name
```
![Image alt](https://github.com/Edo1993/otus_9/raw/master/13.png)

Наличие успешно собранного образа:
```
docker images | grep '<имя>'
docker ps -a
```
Залезть в контейнер и покопаться внутри 
```
docker exec -it container_name sh
```

Перед тем как запушить готовый образ, надо сделать:
```
docker login
docker tag YOURIMAGE YOUR_DOCKERHUB_NAME/YOURIMAGE
```
потом
```
docker push YOUR_DOCKERHUB_NAME/YOURIMAGE
```
# *Определите разницу между контейнером и образом*

   Docker-образ — это read-only шаблон, из которого создается контейнер. Docker позволяет создавать новые образы, обновлять существующие, скачивать образы, созданные другими людьми. Образы — это компонента сборки docker-а.
   
   Каждый контейнер создается из образа, образ говорит docker-у, что находится в контейнере, какой процесс запустить, когда запускается контейнер и другие конфигурационные данные. Контейнеры могут быть созданы, запущены, остановлены, перенесены или удалены. Контейнеры — это компонента работы. Когда docker запускает контейнер, он создает уровень для чтения/записи сверху образа (используя union file system), в котором может быть запущено приложение.

# *Можно ли в контейнере собрать ядро?*

В контейнере можно собрать ядро,пример https://github.com/naftulikay/docker-ubuntu-kernel-build
Загрузиться с собранным ядром нельзя, т.к контейнер переиспользует ядро системы.
