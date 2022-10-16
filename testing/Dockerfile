FROM ubuntu:latest

#EXPOSE 8080
VOLUME /var/www/html
#VOLUME /var/lib/mysql

RUN apt update
RUN apt upgrade

ARG DEBIAN_FRONTEND=noninteractive

# Apache2
RUN apt install apache2 -y

# PHP
RUN apt install libapache2-mod-php php php-mysql -y

# MySQL
RUN apt install mysql-server -y

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=wordpress
ENV MYSQL_USER=wpuser
ENV MYSQL_PASSWORD=wppass

RUN mysql -u root -e "CREATE DATABASE wordpress"
RUN mysql -u root -e "CREATE USER 'wpuser'@'127.0.0.1' IDENTIFIED BY 'wppass'"
RUN mysql -u root -e "GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'127.0.0.1'"

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