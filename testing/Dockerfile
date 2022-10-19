FROM ubuntu:latest

EXPOSE 80
VOLUME /var/www/html

RUN apt upgrade
RUN apt update
#RUN apt-get install -y wget 
# previous command: && rm -rf /var/lib/apt/lists/*

ARG DEBIAN_FRONTEND=noninteractive

# ENV APACHE_RUN_DIR /usr/sbin/
# ENV APACHE_CONFDIR /etc/apache2
# ENV APACHE_RUN_USER www-data
# ENV APACHE_RUN_GROUP www-data
# ENV APACHE_PID_FILE /var/run/apache2/apache2.pid
# ENV APACHE_RUN_DIR /var/run/apache2
# ENV APACHE_LOCK_DIR /var/lock/apache2
# ENV APACHE_LOG_DIR /var/log/apache2

RUN apt install apache2 -y

RUN apt install apache2-utils -y

RUN apt install libapache2-mod-php php php-mysql -y

# RUN apt install mysql-server -y

#RUN apt install unzip

# RUN wget -c http://wordpress.org/latest.zip
# RUN unzip latest.zip
# RUN mv wordpress/* .

# RUN touch wp-config.php
# RUN cp wp-config-sample.php wp-config.php

# RUN sed -i 's/database_name_here/wordpress/' wp-config.php
# RUN sed -i 's/username_here/wpuser/' wp-config.php
# RUN sed -i 's/password_here/wppass/' wp-config.php

CMD [ "/usr/sbin/apache2ctl", "-D", "FOREGROUND" ]