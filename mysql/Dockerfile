FROM mysql:latest

# docker run --name db --network=nw -v db_vol:/var/lib/mysql db_img

VOLUME [ "/var/lib/mysql" ]

ENV MYSQL_ROOT_PASSWORD=secret

COPY ./wordpress.sql /docker-entrypoint-initdb.d/

ENTRYPOINT ["docker-entrypoint.sh"]

CMD [ "mysqld" ]