#docker login registry.redhat.io
FROM ubuntu:latest

RUN apt-get update && apt-get install libapr1-dev libaprutil1-dev -y
RUN apt-get update && apt-get install libc6-dev g++ gcc unzip -y
RUN apt-get update && apt-get install build-essential -y
RUN apt-get update && apt-cache search pcre && apt-get install libpcre3-dev -y

COPY ./httpd-2.4.1.tar.gz /home/shared/httpd-2.4.1.tar.gz
WORKDIR /home/shared/
RUN tar xvfz httpd-2.4.1.tar.gz

COPY ./pcre-8.44.zip /home/shared/pcre-8.44.zip
# RUN mkdir /usr/local/pcre
RUN unzip pcre-8.44.zip -d /usr/local/
WORKDIR /usr/local/pcre-8.44
# RUN make
# RUN make install

WORKDIR /home/shared/httpd-2.4.1/
# RUN export PATH="/usr/bin:$PATH"
RUN ./configure --prefix=/usr/local/pcre-8.44/pcre-config
RUN make
RUN make install
RUN  ./configure --prefix=/usr/local/apache --enable-shared=max
RUN make
RUN make install