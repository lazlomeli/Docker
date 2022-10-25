FROM mysql:latest

ENV MYSQL_ALLOW_EMPTY_PASSWORD=1

COPY ./wordpress.sql /docker-entrypoint-initdb.d/

# ubuntu image