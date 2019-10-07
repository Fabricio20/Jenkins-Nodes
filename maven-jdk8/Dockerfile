FROM azul/zulu-openjdk:8

# Install wget + git + ssh
RUN apt-get update && \
    apt-get install -y wget git openssh-server --no-install-recommends

# Install Maven
RUN mkdir -p /opt/maven && \
    wget https://www-us.apache.org/dist/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz -O /opt/maven/apache-maven.tar.gz --no-check-certificate && \
    tar -xf /opt/maven/apache-maven.tar.gz -C /opt/maven && \
    rm -rf /opt/maven/apache-maven.tar.gz && \
    mv /opt/maven/apache-maven-3.6.2/* /opt/maven && \
    rm -rf /opt/maven/apache-maven-3.6.2/ && \
    ln -s /opt/maven/bin/mvn /usr/local/bin/mvn

# Generate Host SSH Keys
RUN ssh-keygen -A

# Create Jenkins user
RUN adduser -uid 1001 --home /home/jenkins --shell /bin/sh --disabled-password --gecos "Jenkins" jenkins
RUN echo "jenkins:jenkins" | chpasswd

RUN mkdir -p /var/run/sshd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
