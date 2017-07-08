FROM ubuntu:16.04


####################
# JAVA
####################
ENV JAVA_VERSION 8
ENV JAVA_HOME /usr/lib/jvm/jdk

# NOTE: wget is required to download the package in the next sections
RUN apt-get update   && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y wget openjdk-$JAVA_VERSION-jdk    && \
    ln -s /usr/lib/jvm/java-$JAVA_VERSION-openjdk-amd64 /usr/lib/jvm/jdk    && \
    rm -rf /var/lib/apt/lists/*



####################
# HBASE
####################
ENV HBASE_VERSION 1.2.4
ENV HBASE_HOME /usr/local/hbase
ENV PATH $PATH:$HBASE_HOME/bin

RUN wget https://archive.apache.org/dist/hbase/$HBASE_VERSION/hbase-$HBASE_VERSION-bin.tar.gz   && \
    tar -xf hbase-$HBASE_VERSION-bin.tar.gz   && \
    rm hbase-$HBASE_VERSION-bin.tar.gz   && \
    mv hbase-$HBASE_VERSION $HBASE_HOME

# Mounting the HBase data folder
VOLUME /data

# Editing the HBase configuration file to use the local filesystem
ADD conf/hbase-site.xml $HBASE_HOME/conf/hbase-site.xml

# zookeeper
EXPOSE 2181
# HBase Master API port
EXPOSE 60000
# HBase Master Web UI
EXPOSE 60010
# Regionserver API port
EXPOSE 60020
# HBase Regionserver web UI
EXPOSE 60030

# Starting HBase
WORKDIR $HBASE_HOME
CMD ["./bin/start-hbase.sh", "master", "start"]