# Jenkins Nodes [![Build Status](https://travis-ci.com/Fabricio20/Jenkins-Nodes.svg?branch=master)](https://travis-ci.com/Fabricio20/Jenkins-Nodes)

This is the Dockerfile for the `java-14` tag.

**Features**:
- Zulu OpenJDK 14
- Maven 3.6.3 [`/opt/maven`]
- Gradle 6.3 [`/opt/gradle`]
- Docker CLI [Mount your Unix Socket to `/var/run/docker.sock`]
- Bash, Wget, Tar, Zip/Unzip, Git

### Notes

If you need, you can mount your `settings.xml` to `/home/jenkins/.m2/`.

You can mount your SSH `authorized_keys` file (for SSH Keys Login) to `/home/jenkins/.ssh/`.

Password authentication is disabled for these images.

Maintainers:
- Fabricio20
