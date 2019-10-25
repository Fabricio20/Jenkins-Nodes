FROM node

# Install wget + git + ssh
RUN apt-get update && \
    apt-get install -y wget git openssh-server ca-certificates tar --no-install-recommends && \
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
RUN adduser -uid 1001 --gid 999 --home /home/jenkins --shell /bin/sh --disabled-password --gecos "Jenkins" jenkins && \
    sed -i "s/.*RSAAuthentication.*/RSAAuthentication yes/g" /etc/ssh/sshd_config && \
    sed -i "s/.*PubkeyAuthentication.*/PubkeyAuthentication yes/g" /etc/ssh/sshd_config && \
    sed -i "s/.*PasswordAuthentication.*/PasswordAuthentication no/g" /etc/ssh/sshd_config && \
    sed -i "s/.*PermitRootLogin.*/PermitRootLogin no/g" /etc/ssh/sshd_config

RUN mkdir -p /home/jenkins/.ssh/ && \
    touch /home/jenkins/.ssh/authorized_keys && \
    chown -R jenkins:jenkins /home/jenkins/.ssh/ && \
    touch /var/run/docker.sock && \
    chown -R jenkins:jenkins /var/run/docker.sock

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
