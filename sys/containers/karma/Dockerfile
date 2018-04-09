FROM ubuntu:14.04

RUN apt-get update && \
	apt-get install -y wget software-properties-common && \
	add-apt-repository ppa:webupd8team/java && apt-get update && \
	echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections && \
	echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections && \
	apt-get install -y oracle-java8-installer


RUN	wget https://github.com/usc-isi-i2/Web-Karma/archive/v2.053.tar.gz && \
	tar -xf v2.053.tar.gz && \
	wget http://mirrors.koehn.com/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz && \
	tar -xf apache-maven-3.3.9-bin.tar.gz && \
	rm v2.053.tar.gz apache-maven-3.3.9-bin.tar.gz

ENV PATH /apache-maven-3.3.9/bin:$PATH
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

RUN cd /Web-Karma-2.053 && mvn clean install -Dmaven.test.skip=true
# jetty package is not installed by mvn install
RUN cd /Web-Karma-2.053/karma-web && mvn jetty:help

# install offline mode
RUN cd /Web-Karma-2.053/karma-offline && mvn install -P shaded

# max perm size 128m was remove in java 8
ENV MAVEN_OPTS "-Xmx4096m"

WORKDIR /Web-Karma-2.053/karma-web
CMD ["mvn", "jetty:run"]
