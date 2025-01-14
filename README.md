# Java Application Deployment with Tomcat and Maven

This repository contains the practical exercise for deploying a Java application using Tomcat and Maven. The project demonstrates how to configure a Java development environment, build the application with Maven, and deploy it to a Tomcat server.

## 1 - Configure VM

The first step is configuring the virtual machine with Vagrant to install the different services that are going to be used: Tomcat and OpenJDK (Java development kit).
A new group and a new user are going to be added.

After starting the service, Tomcat is proved that is working:

```
sudo systemctl status tomcat9
```
