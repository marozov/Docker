Все дальнейшие действия были проверены при использовании
```
docker-compose --version
Docker Compose version v2.6.1
```
```
docker --version
Docker version 20.10.17
```
Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx)
Определите разницу между контейнером и образом Вывод опишите в домашнем задании.
Ответьте на вопрос: Можно ли в контейнере собрать ядро?
Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.


```
Теоретические вопросы

Определите разницу между контейнером и образом.

Есть несколько объяснений:

Образ это аналог образа виртуальной машины, а контейнер это экземпляр этого образа

Образ это как исполняемый файл, а контейнер как процесс

Ответьте на вопрос: Можно ли в контейнере собрать ядро?
В контейнере можно собрать ядро. Загрузиться с собранным ядром нельзя, т.к контейнер использует ядро системы.
```
Практическая часть

Создаем свой кастомный образ на базе alpine
Создаем отдельную директорию и кладем туда два файла:

Создаем файл Dockerfile (во вложении)

Создаем файл index.html с измененным содержимым (этот файл будет импортирован в образ при создании)

После чего собираем наш образ командой sudo docker build -t marozov/test:test .

Далее можем запустить наш контейнер командой docker run -d -p 12345:81 marozov/test:test

Видим наш образы и наши контейнеры:
```
marozov@imac-marozov Docker % docker images

REPOSITORY                                                TAG                                                                          IMAGE ID       CREATED         SIZE
test                                                      latest                                                                       a83cd4698c30   2 hours ago     204MB
marozov/test                                              test                                                                         a83cd4698c30   2 hours ago     204MBhours ago     204MB
mhiro2/kea-dhcp-server                                    latest                                                                       779cef996b34   4 years ago     69.5MB
```
```
marozov@imac-marozov Docker % docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                    NAMES
c50259d69b52   marozov/test:test               "nginx -g 'daemon of…"   8 seconds ago    Up 7 seconds    80/tcp, 443/tcp, 0.0.0.0:12345->81/tcp   stoic_galois
e3ba3997fedf   test                            "nginx -g 'daemon of…"   35 minutes ago   Up 35 minutes   443/tcp, 0.0.0.0:1234->80/tcp            focused_wright
faba096575ac   mhiro2/kea-dhcp-server:latest   "/usr/local/sbin/kea…"   9 days ago       Up 9 days                                                agitated_dubinsky
```

Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий
Ссылка на репозиторий - https://hub.docker.com/repository/docker/marozov/test

Выполняем команду docker login, и вводим логин и пароль от нашего зарегистрированного аккаунта из docker-hub:
```
[root@borg-server docker]# docker login
```
Login Succeeded
```
Далее делаем sudo docker push marozov/test:test
```
```
The push refers to repository [docker.io/marozov/test]
30d9f5d4d1a7: Pushed
bb72eb146332: Pushed
904d387f3521: Pushed
421cd0da9468: Pushed
24302eb7d908: Pushed
test: digest: sha256:e87918bd04c04f88f828f22565f66ed41370bf37b03953821f9e5b1292df865f size: 1365
```
Образ - это шаблон, на основе которого создается контейнер, существует отдельно и не может быть изменен. Контейнеры — это компонента работы. Основное различие между образом и контейнером — в доступном для записи верхнем слое. Чтобы создать контейнер, Docker берет образ, добавляет доступный для записи верхний слой и инициализирует различные параметры (сетевые порты, имя контейнера, идентификатор и лимиты ресурсов).

