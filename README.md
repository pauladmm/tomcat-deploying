# Java Application Deployment with Tomcat and Maven

This repository contains the practical exercise for deploying a Java application using Tomcat and Maven. The project demonstrates how to configure a Java development environment, build the application with Maven, and deploy it to a Tomcat server.

## 1 - Configure VM

The first step is configuring the virtual machine with Vagrant to install the different services that are going to be used: Tomcat, OpenJDK (Java development kit), Tomcat administrator
A new group and a new user are going to be added.

After starting the service, Tomcat is proved that is working:

```
sudo systemctl status tomcat9
```

## 2 - Administrator Configuration

The user "alumno" is defined to have complete access to all administrative and management functionalities (roles="admin,admin-gui,manager,manager-gui"). The tomcat-users.xml file is modified.
With this credentials, this user could access to <http://localhost:8080/manager/html/>

![Tomcat GUI](/files/img/tomcat-management-gui.PNG)

The context.xml file is modified to allow remote control (any IP address).

```
allow="\d+\.\d+\.\d+\.\d+"
```
