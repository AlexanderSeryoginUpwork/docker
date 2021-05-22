# https://hub.docker.com/r/phpmyadmin/phpmyadmin/
FROM phpmyadmin/phpmyadmin
RUN docker run --name myadmin -d --link mysql_db_server:db -p 8088:80 phpmyadmin
