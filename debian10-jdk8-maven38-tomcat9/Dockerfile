FROM debian:buster

USER root
RUN apt-get update
RUN apt-get install -y wget

RUN mkdir /usr/local/web

############
# Oracle JDK
############

# Preparation

ENV JAVA_VERSION 8u41
ENV JAVA_BUILD 04
ENV JAVA_HOME /usr/local/web/jdk-${JAVA_VERSION}-b${JAVA_BUILD}

# Installation

RUN cd /tmp
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.java.net/openjdk/jdk${JAVA_VERSION}/ri/openjdk-${JAVA_VERSION}-b${JAVA_BUILD}-linux-x64-14_jan_2020.tar.gz
RUN mkdir jdk-${JAVA_VERSION}-linux-x64
RUN tar -zxvf openjdk-${JAVA_VERSION}-b${JAVA_BUILD}-linux-x64-14_jan_2020.tar.gz --directory jdk-${JAVA_VERSION}-linux-x64 --strip-components=1
RUN mv jdk-${JAVA_VERSION}-linux-x64 ${JAVA_HOME}
ENV PATH ${PATH}:${JAVA_HOME}/bin

# Cleanup

RUN rm openjdk-${JAVA_VERSION}-b${JAVA_BUILD}-linux-x64-14_jan_2020.tar.gz
RUN unset JAVA_VERSION

#######
# Maven
#######

# Preparation

ENV MAVEN_VERSION 3.8.3
ENV MAVEN_HOME /usr/local/web/maven-${MAVEN_VERSION}

# Installation

RUN cd /tmp
RUN wget https://dlcdn.apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz
RUN mkdir maven-${MAVEN_VERSION}
RUN tar -zxvf apache-maven-${MAVEN_VERSION}-bin.tar.gz --directory maven-${MAVEN_VERSION} --strip-components=1
RUN mv maven-${MAVEN_VERSION} ${MAVEN_HOME}
ENV PATH ${PATH}:${MAVEN_HOME}/bin

# Cleanup

RUN rm apache-maven-${MAVEN_VERSION}-bin.tar.gz
RUN unset MAVEN_VERSION

#########
# Testing
#########

RUN env
RUN java -version
RUN javac -version
RUN mvn -version

########
# Tomcat
########

# Preparation

ENV TOMCAT_MAJOR 9
ENV TOMCAT_VERSION 9.0.54
ENV TOMCAT_HOME /usr/local/web/tomcat-${TOMCAT_VERSION}

# Installation

RUN cd /tmp
RUN wget https://dlcdn.apache.org/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz
RUN mkdir tomcat-${TOMCAT_VERSION}
RUN tar -zxvf apache-tomcat-${TOMCAT_VERSION}.tar.gz --directory tomcat-${TOMCAT_VERSION} --strip-components=1
RUN mv tomcat-${TOMCAT_VERSION} ${TOMCAT_HOME}
ENV CATALINA_HOME ${TOMCAT_HOME}
ENV PATH ${PATH}:${CATALINA_HOME}/bin

# Cleanup

RUN rm apache-tomcat-${TOMCAT_VERSION}.tar.gz
RUN unset TOMCAT_MAJOR
RUN unset TOMCAT_VERSION
RUN unset TOMCAT_HOME