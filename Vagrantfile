# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "debian/bullseye64"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.provision "shell", inline: <<-SCRIPT

  # Install services
  apt-get update
  apt-get install
  apt install -y tomcat9 openjdk-11-jdk tomcat9-admin maven

  # Add group 
  groupadd tomcat9

  # Add user tomcat9
  useradd -s /bin/false -g tomcat9 -d /etc/tomcat9 tomcat9

  # Modify users and permission configuration and remote access control for Tomcat deploy
  # Modify server block and POM for Maven deploy
  cp /vagrant/files/tomcat-users.xml /etc/tomcat9/tomcat-users.xml
  cp /vagrant/files/context.xml /usr/share/tomcat9-admin/host-manager/META-INF/context.xml
  cp /vagrant/files/settings.xml /etc/maven/settings.xml 
  cp /vagrant/files/pom.xml /home/vagrant/myapp/myapp-war/pom.xml

  # Restart service
  systemctl restart tomcat9
SCRIPT


end
