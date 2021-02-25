FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends software-properties-common && \
    apt-get install --no-install-recommends -y openjdk-8-jdk && \
    rm -rf /var/cache/openjdk-8-jdk && \
    echo "networkaddress.cache.ttl=60" >> /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/security/java.security && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/

RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000

COPY elasticsearch-6.1.5-SNAPSHOT.tar.gz /opt/
RUN mkdir /usr/share/elasticsearch
WORKDIR /usr/share/elasticsearch
RUN tar -zxf /opt/elasticsearch-6.1.5-SNAPSHOT.tar.gz --strip-components=1 && \
    chown -R elasticsearch:elasticsearch /usr/share/elasticsearch
COPY elasticsearch.yml /usr/share/elasticsearch/config/
COPY logging.yml /usr/share/elasticsearch/config


EXPOSE 9200 9300

USER elasticsearch

ENV PATH=$PATH:/usr/share/elasticsearch/bin

CMD ["elasticsearch"]

HEALTHCHECK --interval=10s --timeout=5s --start-period=1m --retries=5 CMD curl -I -f --max-time 5 http://localhost:9200 || exit 1


