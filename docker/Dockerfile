FROM debian:buster-slim
ARG DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install ca-certificates -y && apt clean

COPY couchdb.gpg /etc/apt/trusted.gpg.d/couchdb.gpg
RUN echo "deb https://apache.jfrog.io/artifactory/couchdb-deb/ buster main" > /etc/apt/sources.list.d/couchdb.list
RUN echo "Package: couchdb\nPin: version 3.1.0~buster\nPin-Priority: 999" > /etc/apt/preferences.d/couchdb

RUN apt update && apt install couchdb python3 python3-pip -y && apt clean && \
 python3 -m pip install couchdb boto3 && \
 apt remove python3-pip -y && apt autoremove -y && apt clean

RUN rm -rf /etc/couchdb/ && ln -nsf /opt/couchdb/etc/ /etc/couchdb && ln -nsf /opt/couchdb/bin/couchdb /usr/local/bin/

#USER 65534
