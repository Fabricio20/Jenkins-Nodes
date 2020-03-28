# Jenkins Nodes [![Build Status](https://travis-ci.com/Fabricio20/Jenkins-Nodes.svg?branch=master)](https://travis-ci.com/Fabricio20/Jenkins-Nodes)

These images are Jenkins SSH Nodes that you can use to run your builds on.

### Tags:

- `java-8` Build node with `zulu-8`, `maven`, `gradle`, `docker-cli`, `wget`, `bash`.
- `java-11` Build node with `zulu-11`, `maven`, `gradle`, `docker-cli`, `wget`, `bash`.
- `java-13` Build node with `zulu-13`, `maven`, `gradle`, `docker-cli`, `wget`, `bash`.
- `java-14` Build node with `zulu-14`, `maven`, `gradle`, `docker-cli`, `wget`, `bash`.

### Legacy Tags:

- `gradle-jdk13` Build node with gradle and zulu-jdk13
- `gradle-jdk11` Build node with gradle and zulu-jdk11
- `gradle-jdk8` Build node with gradle and zulu-jdk8
- `maven-jdk13` Build node with maven and zulu-jdk13
- `maven-jdk11` Build node with maven and zulu-jdk11
- `maven-jdk8` Build node with maven and zulu-jdk8

### Notes

All images have gradle/maven installed on `/opt`. (`/opt/maven` and `/opt/gradle`).

If you need, you can mount your `settings.xml` to `/home/jenkins/.m2/`.

You can mount your SSH `authorized_keys` file (for SSH Keys Login) to `/home/jenkins/.ssh/`.

Password authentication is disabled for these images.

Maintainers:
- Fabricio20
- Christian Tusset
