FROM zhangluya/ubuntu:22.04
#FROM ubuntu:latest

LABEL maintainer="Jesse" service="Jenkins" version="latest stable Jenkins WAR file"

ENV JENKINS_HOME="/usr/local/jenkins"
ENV JAVA_HOME=/usr/local/jdk-17.0.5
ENV PATH=$JAVA_HOME/bin:$PATH
ENV DEBIAN_FRONTEND="noninteractive"
ENV TZ=Asia/Shanghai

# Install JDK && Jenkins
# https://download.oracle.com/java/17/archive/jdk-17.0.5_linux-x64_bin.tar.gz
# http://mirrors.jenkins.io/war-stable/latest/jenkins.war
WORKDIR /usr/local/
RUN echo "1.Start installing JDK......" \
    && apt update \
    && apt upgrade -y \
    && apt install wget font-manager  tzdata -y \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && wget https://software-mirrors.hk.ufileos.com/java/17/archive/jdk-17.0.5_linux-x64_bin.tar.gz \
    && tar zvfx jdk-17.0.5_linux-x64_bin.tar.gz \
    && rm -rf jdk-17.0.5_linux-x64_bin.tar.gz \
    && echo "Start installing jenkins......" \
    && mkdir -p ${JENKINS_HOME} \
    && wget https://software-mirrors.hk.ufileos.com/jenkins/war-stable/2.361.4/jenkins.war \
    && /bin/mv jenkins.war ${JENKINS_HOME} \
    && apt remove -y wget && apt autoremove -y \ 
    && rm -rf /var/lib/apt/lists/*


COPY ./config/docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod a+x /docker-entrypoint.sh
EXPOSE 8080

ENTRYPOINT ["/docker-entrypoint.sh"]

