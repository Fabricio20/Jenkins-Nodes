FROM azul/zulu-openjdk:11

# Install wget + unzip + git + ssh
RUN apt-get update && \
    apt-get install -qy wget unzip git openssh-server --no-install-recommends && \
# Install Gradle
    mkdir -p /opt/gradle && \
    wget https://services.gradle.org/distributions/gradle-5.6.2-bin.zip -O /opt/gradle/gradle.zip --no-check-certificate && \
    unzip /opt/gradle/gradle.zip -d /opt/gradle && \
    rm -rf /opt/gradle/gradle.zip && \
    mv /opt/gradle/gradle-5.6.2/* /opt/gradle && \
    rm -rf /opt/gradle/gradle-5.6.2/ && \
    ln -s /opt/maven/bin/gradle /usr/local/bin/gradle && \
# Uninstall tools
    apt-get purge wget unzip -qy && \
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
