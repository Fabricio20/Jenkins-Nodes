# Jenkins Nodes [![Build Status](https://travis-ci.com/Fabricio20/Jenkins-Nodes.svg?branch=master)](https://travis-ci.com/Fabricio20/Jenkins-Nodes)

These images are Jenkins SSH Nodes that you can use to run your builds on.

### Tags:

- `gradle-jdk11` Build node with gradle and zulu-jdk11
- `gradle-jdk8` Build node with gradle and zulu-jdk8
- `maven-jdk11` Build node with maven and zulu-jdk11
- `maven-jdk8` Build node with maven and zulu-jdk8

### Notes

All images have gradle/maven installed on `/opt`. (`/opt/maven` and `/opt/gradle`).

If you need, you can mount your `settings.xml` to `/opt/maven/conf/settings.xml`.

The user:password for these nodes is `jenkins:jenkins`. These are NOT intended to be run open on the internet.
Fork and change the password if you believe you need these nodes exposed to the internet.

Maintainers:
- Fabricio20
