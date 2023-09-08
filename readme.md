1) Написать кастомный Dockerfile для nginx:
- базовый образ - debian
- с помощью RUN установить nginx
- скопировать index.html в /usr/share/nginx/html/index.html с хоста в контейнер
- скопировать vhost.conf в /etc/nginx/conf.d/vhost.conf с хоста в контейнер
 - вывесить порт 80 контейнера на порт 8080 хоста
 - собрать image
 - запустить из него контейнер
 - скопировать index.html в папку /var/www/html на хосте, изменить в нем строку ```Hello everyone, This is running via Docker container``` на ```Hello everyone, This is running on host```
 - добавить в /etc/nginx/sites-enabled vhost.conf, изменить в нем ```root /usr/share/nginx/html;``` на ```root /var/www/html;```, выполнить
```
sudo nginx -t
sudo nginx -s reload
```

Итоговый результат: команды
```
curl 127.0.0.1:8080
curl 127.0.0.1:80
```
отдают соответсвующие разметки:
- 8080 - ```Hello everyone, This is running via Docker container```
- 80 - ```Hello everyone, This is running on host```

2) Дан код на golang - простейший веб-сервер, слушается на порту 3000 (файл main.go). Нужно написать Dockerfile, в котором будет собран бинарный файл (команда ```go build -o /path/to/binary_file /path/to/main.go```) и запустить из него контейнер.
Итоговый результат: команда 
```
curl 127.0.0.1:3000 
```
отдает Hello World
