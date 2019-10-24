FROM azul/zulu-openjdk:13

# Install wget + git + ssh
RUN apt-get update && \
    apt-get install -y wget git openssh-server ca-certificates tar unzip --no-install-recommends && \
# Install Maven
    mkdir -p /opt/maven && \
    wget https://www-us.apache.org/dist/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz -O /opt/maven/apache-maven.tar.gz --no-check-certificate && \
    tar -xf /opt/maven/apache-maven.tar.gz -C /opt/maven && \
    rm -rf /opt/maven/apache-maven.tar.gz && \
    mv /opt/maven/apache-maven-3.6.2/* /opt/maven && \
    rm -rf /opt/maven/apache-maven-3.6.2/ && \
    ln -s /opt/maven/bin/mvn /usr/local/bin/mvn && \
# Install Gradle
    mkdir -p /opt/gradle && \
    wget https://services.gradle.org/distributions/gradle-5.6.2-bin.zip -O /opt/gradle/gradle.zip --no-check-certificate && \
    unzip /opt/gradle/gradle.zip -d /opt/gradle && \
    rm -rf /opt/gradle/gradle.zip && \
    mv /opt/gradle/gradle-5.6.2/* /opt/gradle && \
    rm -rf /opt/gradle/gradle-5.6.2/ && \
    ln -s /opt/maven/bin/gradle /usr/local/bin/gradle && \
# Install Docker
    wget https://download.docker.com/linux/static/stable/x86_64/docker-19.03.4.tgz --no-check-certificate && \
    tar --strip-components=1 -xvzf docker-19.03.4.tgz -C /usr/local/bin && \
# Uninstall tools
    apt-get purge wget -qy && \
    apt-get autoremove -qy

# Generate Host SSH Keys
RUN ssh-keygen -A && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd && \
    mkdir -p /var/run/sshd

# Create Jenkins user
RUN adduser -uid 1001 --home /home/jenkins --shell /bin/sh --disabled-password --gecos "Jenkins" jenkins && \
    sed -i "s/.*RSAAuthentication.*/RSAAuthentication yes/g" /etc/ssh/sshd_config && \
    sed -i "s/.*PubkeyAuthentication.*/PubkeyAuthentication yes/g" /etc/ssh/sshd_config && \
    sed -i "s/.*PasswordAuthentication.*/PasswordAuthentication no/g" /etc/ssh/sshd_config && \
    sed -i "s/.*PermitRootLogin.*/PermitRootLogin no/g" /etc/ssh/sshd_config

ADD settings.xml /home/jenkins/.m2/

RUN mkdir -p /home/jenkins/.ssh/ && \
    touch /home/jenkins/.ssh/authorized_keys && \
    chown -R jenkins:jenkins /home/jenkins/.m2/ && \
    chown -R jenkins:jenkins /home/jenkins/.ssh/ && \
    touch /var/run/docker.sock && \
    chown -R jenkins:jenkins /var/run/docker.sock

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
