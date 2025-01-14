# Java Application Deployment with Tomcat and Maven

This repository contains the practical exercise for deploying a Java application using Tomcat and Maven. The project demonstrates how to configure a Java development environment, build the application with Maven, and deploy it to a Tomcat server.

## 1 - Configure VM

The first step is configuring the virtual machine with Vagrant to install the different services that are going to be used: **Tomcat, OpenJDK (Java development kit), Tomcat administrator**.
A new group and a new user are going to be added.

After starting the service, Tomcat is proved that is working:

```
sudo systemctl status tomcat9
```

## 2 - Administrator Configuration

The user _alumno_ is defined to have complete access to all administrative and management functionalities **(roles="admin,admin-gui,manager,manager-gui")**. The **tomcat-users.xml** file is modified.
With this credentials, this user could access to <http://localhost:8080/manager/html/>

![Tomcat GUI](/files/img/tomcat-management-gui.PNG)

The **context.xml** file is modified to allow remote control (any IP address).

```
allow="\d+\.\d+\.\d+\.\d+"
```

## 2 - GUI Deployment

Through the Tomcat GUI a Web Application Archive can be deployed just uploading a **.war** file in the previous link (/manager/html).
![GUI Deployment](/files/img/gui-deployment.PNG)

## 3 - Maven Configuration

Maven is a tool to build projects automatically based in Java. In this practice, the deployment is going to be maden by command line.
In order to install Maven, the package was added to the vagrant provision.

Next, new role _manager-script_ and new user was added in **tomcat-users.xml**. It is recommended not to use the same user for GUI deployment and Maven's one.

The server block in **settings.xml** file is modified in order to add the user created previously.

### 3.1 - App Generation

In a personal directory inside de machine, an app called **myapp-war** was generated with the followed command:

```
mvn archetype:generate -DgroupId=org.zaidinvergeles \
-DartifactId=myapp-war \
-DarchetypeArtifactId=maven-archetype-webapp \
-DinteractiveMode=false

```

![myapp built](/files/img/myapp-war-built.PNG)

### 3.2 - App Deployment

After create the app, a directory was created inside (myapp-war in this case).
In order to specifying the Maven's plugin for Tomcat doing this deployment, the POM is needed to be modified the following way:

```
...

<build>
    <finalName>myapp-war-deployment</finalName>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
          <url>http://localhost:8080/manager/text</url>
          <server>Tomcat</server>
          <path>/despliegue</path>
        </configuration>
      </plugin>
    </plugins>
  </build>

```

In this build block:

- The final **app name** is specified _myapp-war-deployment_ (.jar).
- The **deployment url** has to match with the localhost.
- The **server name** has to be correlative with the name given in the settings.xml file.
- A **path** to access the app has to be given.

Finally, to deploy the app this command was used:

```
mvn tomcat7:deploy
```

![myapp deployed](/files/img/myapp-deployed-maven.PNG)

## 4 - Another App Deployment (Rock Scissor Paper)

To keep practising, this time an app from Github was cloned to the machine, and the branch _patch-1_ was choosen to avoid conflicts:

```
git clone https://github.com/cameronmcnz/rock-paper-scissors.git

git checkout patch-1

```

This time POM file was modified to add a pluggin block with this Tomcat server data, and adding the path **/rsp** to access the app.

```
<plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.2</version>
          <configuration>
            <url>http://localhost:8080/manager/text</url>
            <server>Tomcat</server>
            <path>/rsp</path>
        </configuration>
      </plugin>
```

Next, the app was deployed with:

```
mvn tomcat7:deploy
```

![RSP deployed](/files/img/rock-scissors-paper-deployment.PNG)

The App:

![RSP App](/files/img/rsp-app.PNG)
