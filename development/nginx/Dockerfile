FROM nginx:1.10

ADD ./docker/development/nginx/default.conf /etc/nginx/conf.d/default.conf

COPY ./docker/development/nginx/ssl/ssl-cert-snakeoil.key /etc/nginx/ssl/ssl-cert-snakeoil.key
COPY ./docker/development/nginx/ssl/ssl-cert-snakeoil.pem /etc/nginx/ssl/ssl-cert-snakeoil.pem

WORKDIR /var/www/html
