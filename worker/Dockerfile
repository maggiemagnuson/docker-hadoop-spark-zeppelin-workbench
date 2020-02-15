FROM bde2020/spark-base:2.1.0-hadoop2.8-hive-java8

COPY worker.sh /

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

RUN ln -s /usr/bin/pip3 /usr/bin/pip \
    && ln -s /usr/bin/python3.7 /usr/bin/python

ENV SPARK_WORKER_WEBUI_PORT 8081
ENV SPARK_WORKER_LOG /spark/logs
ENV SPARK_MASTER "spark://spark-master:7077"
# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1

EXPOSE 8081

CMD ["/bin/bash", "/worker.sh"]
