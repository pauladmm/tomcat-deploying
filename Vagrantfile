# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "debian/bullseye64"
  config.vm.provision "shell", inline: <<-SCRIPT

  # Install services
  apt-get update
  apt-get install
  apt install -y tomcat9 openjdk-11-jdk

  # Add group 
  groupadd tomcat9

  # Add user tomcat9
  useradd -s /bin/false -g tomcat9 -d /etc/tomcat9 tomcat9

  # Restart service
  systemctl restart tomcat9
SCRIPT


end
