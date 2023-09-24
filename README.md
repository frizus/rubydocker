Пример `.env`:

```shell
COMPOSE_PROJECT_NAME=ruby
INTERFACE=127.0.0.1
CONTAINER_PATH=/home/me/ruby-container
SITE_DIR=app
NETWORK=ruby_network
SUBNET=11.100.0.0/24
APP_USER_UID=1000
APP_GROUP_GID=1000
```

### Чтобы создать проект Rails

1. В `docker-compose.yml` закоментировать
```yml
   command: bash -c "rm -f /tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
```

2. Надо в `ruby/Dockerfile` закомментировать
```Dockerfile
ENTRYPOINT ["docker-entrypoint.sh"]
```
и
```Dockerfile
CMD ["rails", "server", "-b", "0.0.0.0"]
```

3. Раскомментировать последнюю строку
```Dockerfile
#ENTRYPOINT ["tail", "-f", "/dev/null"]
```

4. `docker-compose build --no-cache`
5. `docker-compose up -d`
6. Зайти через терминал, в папке `/usr/src/app` написать `rails new ./`
7. Дождаться создания проекта
8. `docker-compose down`
8. Откатить изменения `3.`, `2.`, `1.`, удалить Image `ruby-ruby`
9. `docker-compose build --no-cache`
10. `docker-compose up -d`
11. Проект доступен по http://localhost:3000/