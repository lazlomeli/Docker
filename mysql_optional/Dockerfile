FROM ubuntu:latest

LABEL author="Lazlo Meli Fernández <lazlomeli@gmail.com>"

EXPOSE 3306

VOLUME [ "/var/lib/mysql" ]

RUN apt update && \
    apt install -y mysql-server && \
    apt-get install -y gosu

ENV MYSQL_ROOT_PASSWORD=secret

COPY ./wordpress.sql /docker-entrypoint-initdb.d/

COPY ./docker-entrypoint.sh /usr/local/bin/

COPY ./entrypoint.sh /

RUN chmod +x entrypoint.sh && \
    chmod +x /docker-entrypoint-initdb.d/wordpress.sql && \
    chmod +x /usr/local/bin/docker-entrypoint.sh

CMD [ "docker-entrypoint.sh", "mysqld" ]