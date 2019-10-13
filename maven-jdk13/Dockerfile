FROM azul/zulu-openjdk:13

# Install wget + git + ssh
RUN apt-get update && \
    apt-get install -y wget git openssh-server ca-certificates --no-install-recommends && \
# Install Maven
    mkdir -p /opt/maven && \
    wget https://www-us.apache.org/dist/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz -O /opt/maven/apache-maven.tar.gz --no-check-certificate && \
    tar -xf /opt/maven/apache-maven.tar.gz -C /opt/maven && \
    rm -rf /opt/maven/apache-maven.tar.gz && \
    mv /opt/maven/apache-maven-3.6.2/* /opt/maven && \
    rm -rf /opt/maven/apache-maven-3.6.2/ && \
    ln -s /opt/maven/bin/mvn /usr/local/bin/mvn && \
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
    chown -R jenkins:jenkins /home/jenkins/.ssh/

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
