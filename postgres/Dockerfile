ARG PG_MAJOR=17
FROM postgres:$PG_MAJOR
ARG PGBIN=/usr/lib/postgresql/$PG_MAJOR/bin
ENV PG_MAX_WAL_SENDERS=8
ENV PG_WAL_KEEP_SEGMENTS=8
COPY ../debian.list /etc/apt/sources.list.d/debian.list
RUN apt-get update -y
RUN apt install apt-transport-https ca-certificates
RUN apt-get install -y python3 curl
RUN apt-get install -y python3-psycopg2 python3-pip
RUN pip3 install patroni[zookeeper] --break-system-package
COPY postgres/postgres0.yml /postgres0.yml
COPY postgres/postgres1.yml /postgres1.yml
RUN echo "PATH=/usr/lib/postgresql/$PG_MAJOR/bin:\$PGBIN:\$PATH" >> /etc/profile
CMD ["patroni.py"]
