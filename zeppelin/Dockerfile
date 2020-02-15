FROM bde2020/spark-base:2.1.0-hadoop2.8-hive-java8
MAINTAINER Ivan Ermilov <ivan.s.ermilov@gmail.com>

ENV APACHE_SPARK_VERSION 2.1.0
ENV APACHE_HADOOP_VERSION 2.8.0
ENV ZEPPELIN_VERSION 0.8.1
ENV ZEPPELIN_PORT 8888

RUN rm /etc/apt/sources.list
RUN echo "deb http://security.debian.org/ jessie/updates main" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://security.debian.org/ jessie/updates main" | tee -a /etc/apt/sources.list
RUN echo "deb http://archive.debian.org/debian/ jessie-backports main" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://archive.debian.org/debian/ jessie-backports main" | tee -a /etc/apt/sources.list
RUN echo "deb http://archive.debian.org/debian/ jessie main contrib non-free" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://archive.debian.org/debian/ jessie main contrib non-free" | tee -a /etc/apt/sources.list
RUN echo "deb http://ftp.us.debian.org/debian/ testing main" | tee -a /etc/apt/sources.list
RUN echo "Acquire::Check-Valid-Until false;" | tee -a /etc/apt/apt.conf.d/10-nocheckvalid
RUN echo 'Package: *\nPin: origin "archive.debian.org"\nPin-Priority: 500' | tee -a /etc/apt/preferences.d/10-archive-pin

RUN apt-get update && apt-get install -y python3.6 python3-pip

RUN pip3 install numpy pandasql scipy requests

RUN apt-get install -y wget
RUN wget -q -O /tmp/zeppelin.tgz http://archive.apache.org/dist/zeppelin/zeppelin-0.8.1/zeppelin-0.8.1-bin-all.tgz \
    && tar -xzvf /tmp/zeppelin.tgz -C /opt/ \
    && mv /opt/zeppelin-* /opt/zeppelin \
    && rm /tmp/zeppelin.tgz

RUN ln -s /usr/bin/pip3 /usr/bin/pip \
    && ln -s /usr/bin/python3.7 /usr/bin/python

ENV SPARK_SUBMIT_OPTIONS "--jars /opt/zeppelin/sansa-examples-spark-2016-12.jar"

WORKDIR /opt/zeppelin

CMD ["/opt/zeppelin/bin/zeppelin.sh"]
