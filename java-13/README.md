# Jenkins Nodes [![Build Status](https://travis-ci.com/Fabricio20/Jenkins-Nodes.svg?branch=master)](https://travis-ci.com/Fabricio20/Jenkins-Nodes)

This is the Dockerfile for the `java-13` tag.
<br>
**Features**:
- Maven 3.6.2 [`/opt/maven`]
- Gradle 5.6.2 [`/opt/gradle`]
- Docker CLI [Mount your Unix Socket to `/var/run/docker.sock`]

### Notes

If you need, you can mount your `settings.xml` to `/home/jenkins/.m2/`.

You can mount your SSH `authorized_keys` file (for SSH Keys Login) to `/home/jenkins/.ssh/`.

Password authentication is disabled for these images.

Maintainers:
- Fabricio20