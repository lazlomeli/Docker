FROM ubuntu:latest

EXPOSE 8000
VOLUME /var/www/html

RUN apt update
RUN apt upgrade
RUN apt-get install -y wget && rm -rf /var/lib/apt/lists/*

ARG DEBIAN_FRONTEND=noninteractive

# Apache2
RUN apt update
RUN apt install apache2 -y

# PHP
RUN apt install libapache2-mod-php php php-mysql -y

# MySQL
RUN apt install mysql-server -y

#
RUN apt install unzip

# Wordpress
RUN wget -c http://wordpress.org/latest.zip
RUN unzip latest.zip
RUN mv wordpress/* .

# Edit
RUN touch wp-config.php
RUN cp wp-config-sample.php wp-config.php

RUN sed -i 's/database_name_here/wordpress/' wp-config.php
RUN sed -i 's/username_here/wpuser/' wp-config.php
RUN sed -i 's/password_here/wppass/' wp-config.php

CMD [ "echo", "Done" ]