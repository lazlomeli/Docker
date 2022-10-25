FROM ubuntu:latest

EXPOSE 80
VOLUME /var/www/html
WORKDIR /var/www/html

ARG DEBIAN_FRONTEND=noninteractive

RUN apt upgrade
RUN apt update
RUN apt-get install -y wget 

RUN apt install apache2 -y
RUN apt install apache2-utils -y
RUN apt install libapache2-mod-php php php-mysql -y

RUN apt install unzip
RUN wget -c http://wordpress.org/latest.zip
RUN unzip latest.zip
RUN mv wordpress/* .
RUN rm index.html

RUN touch wp-config.php
RUN cp wp-config-sample.php wp-config.php

RUN sed -i 's/database_name_here/wordpress/' wp-config.php
RUN sed -i 's/username_here/wpuser/' wp-config.php
RUN sed -i 's/password_here/wppass/' wp-config.php
RUN sed -i 's/localhost/webapp_cont/' wp-config.php

CMD [ "/usr/sbin/apache2ctl", "-D", "FOREGROUND" ]