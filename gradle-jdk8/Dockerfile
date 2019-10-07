FROM azul/zulu-openjdk:8

# Install wget + unzip + git + ssh
RUN apt-get update && \
    apt-get install -y wget unzip git openssh-server --no-install-recommends

# Install Gradle
RUN mkdir -p /opt/gradle && \
    wget https://services.gradle.org/distributions/gradle-5.6.2-bin.zip -O /opt/gradle/gradle.zip --no-check-certificate && \
    unzip /opt/gradle/gradle.zip -d /opt/gradle && \
    rm -rf /opt/gradle/gradle.zip && \
    mv /opt/gradle/gradle-5.6.2/* /opt/gradle && \
    rm -rf /opt/gradle/gradle-5.6.2/ && \
    ln -s /opt/maven/bin/gradle /usr/local/bin/gradle

# Generate Host SSH Keys
RUN ssh-keygen -A

# Create Jenkins user
RUN adduser -uid 1001 --home /home/jenkins --shell /bin/sh --disabled-password --gecos "Jenkins" jenkins
RUN echo "jenkins:jenkins" | chpasswd

RUN mkdir -p /var/run/sshd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
