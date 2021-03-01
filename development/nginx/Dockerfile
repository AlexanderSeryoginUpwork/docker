FROM nginx:1.10

ADD default.conf /etc/nginx/conf.d/default.conf

COPY ssl/ssl-cert-snakeoil.key /etc/nginx/ssl/ssl-cert-snakeoil.key
COPY ssl/ssl-cert-snakeoil.pem /etc/nginx/ssl/ssl-cert-snakeoil.pem

WORKDIR /var/www
