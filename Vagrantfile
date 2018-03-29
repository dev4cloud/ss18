# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
  
     vb.memory = "8192"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    
    sudo echo "LANG=en_US.UTF-8" >> /etc/environment
    sudo echo "LANGUAGE=en_US.UTF-8" >> /etc/environment
    sudo echo "LC_ALL=en_US.UTF-8" >> /etc/environment
    sudo echo "LC_CTYPE=en_US.UTF-8" >> /etc/environment
    export DEBIAN_FRONTEND=noninteractive
    sudo add-apt-repository -y ppa:webupd8team/java
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get -y upgrade
    echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections 
    echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
    sudo apt-get -y install oracle-java8-installer
    
    sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11
    sudo apt-get install gnome-icon-theme-full tango-icon-theme
    sudo echo "allowed_users=anybody" > /etc/X11/Xwrapper.config

    sudo /usr/share/debconf/fix_db.pl
    sudo sudo apt-get -y upgrade

    if ! [ -f /opt/eclipse-committers-oxygen-3-linux-gtk-x86_64.tar.gz ]; then
        sudo wget -O /opt/eclipse-committers-oxygen-3-linux-gtk-x86_64.tar.gz http://ftp.fau.de/eclipse/technology/epp/downloads/release/oxygen/3/eclipse-committers-oxygen-3-linux-gtk-x86_64.tar.gz
        cd /opt/ && sudo tar -zxvf eclipse-committers-oxygen-3-linux-gtk-x86_64.tar.gz
    fi

    curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
    sudo apt-get install -y nodejs
    echo "installed node js"

    sudo apt-get -q -y install git

    sudo apt-get -q -y install software-properties-common

    sudo apt-get -q -y install ansible python-pip python-dev libffi-dev libssl-dev

    sudo pip install pytz shade boto boto3




  SHELL

  config.vm.synced_folder "workspace/", "/home/vagrant/workspace/", create: true
end
