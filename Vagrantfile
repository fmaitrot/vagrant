# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |vb|
     vb.gui = true

     vb.memory = "4096"
     vb.cpus = "2"
  end

  config.vm.provision "shell", inline: <<-SHELL

    # Set environment
    sudo echo "LANG=en_US.UTF-8" >> /etc/environment
    sudo echo "LANGUAGE=en_US.UTF-8" >> /etc/environment
    sudo echo "LC_ALL=en_US.UTF-8" >> /etc/environment
    sudo echo "LC_CTYPE=en_US.UTF-8" >> /etc/environment

    # Set keyboard configuration
    sudo loadkeys fr
    sudo setxkbmap fr

    # Install JAVA 8
    sudo add-apt-repository -y ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get -y upgrade
    echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
    echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
    sudo apt-get -y install oracle-java8-installer

    # Install maven 3
    sudo apt-add-repository -y ppa:andrei-pozolotin/maven3
    sudo apt-get update
    sudo apt-get install maven3

    # Install Git
    sudo add-apt-repository -y ppa:git-core/ppa
    sudo apt-get update
    sudo apt-get -y install git

    # Install GUI
    sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11
    sudo apt-get install gnome-icon-theme-full tango-icon-theme

    # Configure GUI
    sudo echo "allowed_users=anybody" > /etc/X11/Xwrapper.config
    xfconf-query -c xsettings -p /Net/ThemeName -s "Xfce-4.6"
    xfconf-query -c xsettings -p /Net/IconThemeName -s "Tango"

    # Install ATOM
    sudo add-apt-repository -y ppa:webupd8team/atom
    sudo apt-get update
    sudo apt-get -y install atom

    # Install CHROME
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
    sudo sh -c 'echo "deb https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
    sudo apt-get update
    sudo apt-get -y install google-chrome-stable

    # Install ECLIPSE
    #sudo wget -O /opt/eclipse-jee-mars-2-linux-gtk-x86_64.tar.gz http://ftp.fau.de/eclipse/technology/epp/downloads/release/mars/2/eclipse-jee-mars-2-linux-gtk-x86_64.tar.gz
    #cd /opt/ && sudo tar -zxvf eclipse-jee-mars-2-linux-gtk-x86_64.tar.gz

    # Install IntelliJ
    sudo wget -O /opt/ideaIU-2016.1.3.tar.gz  https://download.jetbrains.com/idea/ideaIU-2016.1.3.tar.gz
    cd /opt/ && sudo tar -zxvf ideaIU-2016.1.3.tar.gz

    # Add desktop shortcut
    BIN="/opt/idea-IU-145.1617.8/bin"
    sudo echo "[Desktop Entry]\nEncoding=UTF-8\nName=IntelliJ IDEA\nComment=IntelliJ IDEA\nExec=${BIN}/idea.sh\nIcon=${BIN}/idea.png\nTerminal=false\nStartupNotify=true\nType=Application\nCategories=Development;Java;" > /usr/share/applications/IDEA.desktop

  SHELL
end
