version: '3.7'
services:
nginx:
build:
context: docker
dockerfile: nginx/Dockerfile
volumes:
- ./:/var/www
- ./docker/nginx/ssl:/etc/nginx/ssl
ports:
- "????:443" #"8080:443"
links:
- php-fpm
php-fpm:
build:
context: docker
dockerfile: php/Dockerfile
volumes:
- ./:/var/www
links:
- mysql
environment:
- "DB_PORT=3306"
# в Laravel в .env
# DB_HOST=127.0.0.1
# DB_PORT=33061
- "DB_HOST=mysql"
mysql:
# container_name можно не писать.
# Все, что тут сбилжено будет находиться в отдельном нетворке
# и пересечется с другими контейнерами только если совпадут порты
image: mysql:5.7
volumes:
# в линуксе mysql хранится в директории /var/lib/mysql.
# Менять названия папок не надо.
- mysql3_volume:/var/lib/mysql
environment:
- "MYSQL_ROOT_PASSWORD=secret"
- "MYSQL_USER=app"
- "MYSQL_PASSWORD=secret"
- "MYSQL_DATABASE=v8_chrono"
ports:
- "MYSQL_PORT:3306"
phpmyadmin:
image: phpmyadmin/phpmyadmin
environment:
- PMA_ARBITRARY=1
restart: always
#        build:
#            context: docker
#            dockerfile: ./phpmyadmin/Dockerfile
        ports:
            - ????:80
        links:
            - mysql
    node:
        build:
            context: docker
            dockerfile: node/Dockerfile
        volumes:
            - ./:/var/www
        tty: true
#    redis:
#        build:
#            context: docker
#            dockerfile: redis/Dockerfile
#        volumes:
#            - redis_volume:/data

# объявляем, что для mysql существует volume с именем mysqlv
# и что теперь коннектится нужно не на папку, а на volume
# это создаст более независимое и устойчивое поведение
volumes:
mysql3_volume:


# redis
# Внутри папки docker создаю папку redis
# Гуглим образ redis. https://hub.docker.com/_/redis/
# Внутри папки redis создаю Dockerfile   ~ You can create your own Dockerfile that adds a redis.conf from the context into /data/, like so

# В Dockerfile прописываю (взято отсюда https://hub.docker.com/_/redis/)
    # FROM redis
    # COPY redis.conf /usr/local/etc/redis/redis.conf
    # CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]


# Открываем docker-compose.yml (все настройки дублируются и тут, чтоб потом одной командой интерпретатор прошелся по этому файлу и позапускал все, что там прописано)
# Пишем redis:
# Внутри контейнера прописываем настройки
    # build: (что делаем - собираем образ)
        # context: docker (базовая папка docker)
        # dockerfile: redis/Dockerfile (путь к докерфайлу = т.е. откуда брать инструкции типа FROM redis:5.0)
    # volumes:
      # - redis_volume:/data (redis_volume - название контейнера, /data - куда будут сохраняться реальные данные хранимые в редисе)
#
