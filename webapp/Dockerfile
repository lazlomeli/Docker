FROM ubuntu:latest

# docker run --name webapp -p 8000:80 -v webapp_vol:/var/www/html --network=nw webapp_img

LABEL author="Lazlo Meli <lazlomeli@gmail.com>"

EXPOSE 80

VOLUME [ "/var/www/html" ]
WORKDIR /var/www/html

ARG DEBIAN_FRONTEND=noninterac  tive

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2

RUN apt upgrade && \
    apt update && \
    apt-get install -y wget  && \
    apt install -y \
    apache2 \
    apache2-utils \
    php \
    php-mysql \
    wget \
    unzip && \
    wget -c http://wordpress.org/latest.zip && \
    unzip latest.zip && \
    mv wordpress/* . && \
    rm index.html && \
    touch wp-config.php && \
    cp wp-config-sample.php wp-config.php && \
    sed -i 's/database_name_here/wordpress/' wp-config.php && \
    sed -i 's/username_here/root/' wp-config.php && \
    sed -i 's/password_here/secret/' wp-config.php && \
    sed -i 's/localhost/db/' wp-config.php

ENTRYPOINT [ "/usr/sbin/apache2" ]

CMD [ "-D", "FOREGROUND" ]