# -*- mode: ruby -*-
# vi: set ft=ruby :

# This Vagrant file installs Java , sdkman, Intellij , Gradle and Maven onto an Ubuntu UI desktop OS.

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "4096"
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  config.vm.provision "shell", inline: <<-SHELL
    
    sudo echo "LANG=en_US.UTF-8" >> /etc/environment
    sudo echo "LANGUAGE=en_US.UTF-8" >> /etc/environment
    sudo echo "LC_ALL=en_US.UTF-8" >> /etc/environment
    sudo echo "LC_CTYPE=en_US.UTF-8" >> /etc/environment
	# === oracle begin
   sudo apt-get install -y software-properties-common python-software-properties
   echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
   sudo add-apt-repository ppa:webupd8team/java -y
   sudo apt-get update
   sudo apt-get install oracle-java8-installer
   echo "Setting environment variables for Java 8.."
   sudo apt-get install -y oracle-java8-set-default
	# === oracle end
	
	#sudo apt-get install -y openjdk-8-jdk
	sudo apt-get install -y curl   
    sudo apt-get install -y zip   
	
	
	# Ubuntu GUI dependencies
    
    sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11
    sudo apt-get install gnome-icon-theme-full tango-icon-theme
    sudo echo "allowed_users=anybody" > /etc/X11/Xwrapper.config
  
   # sudo wget -O /opt/eclipse-java-luna-SR2-linux-gtk-x86_64.tar.gz http://ftp.fau.de/eclipse/technology/epp/downloads/release/luna/SR2/eclipse-java-luna-SR2-linux-gtk-x86_64.tar.gz
   # cd /opt/ && sudo tar -zxvf eclipse-java-luna-SR2-linux-gtk-x86_64.tar.gz
  SHELL
  
   
   # sdkman avoid the need to setup env variables. , if running manually open a new terminal window to activate changes 
  config.vm.provision "shell", privileged: false, inline: "curl -s http://get.sdkman.io | bash"
  
  # sdk cli install
  config.vm.provision "shell", privileged: false, inline: "source '/home/vagrant/.sdkman/bin/sdkman-init.sh' && yes | sdk install maven 3.3.9"
  config.vm.provision "shell", privileged: false, inline: "source '/home/vagrant/.sdkman/bin/sdkman-init.sh' && yes | sdk install springboot 1.3.6.RELEASE"
  config.vm.provision "shell", privileged: false, inline: "source '/home/vagrant/.sdkman/bin/sdkman-init.sh' && yes | sdk install gradle 2.9"
 
 
    #  install intellij
  config.vm.provision "shell", privileged: true, inline: "cd /opt && wget -O /opt/intellij.tar.gz https://download.jetbrains.com/idea/ideaIC-2016.2.tar.gz && tar xzvf  /opt/intellij.tar.gz " 
  config.vm.provision "shell", privileged: true, inline: "chown -R vagrant /opt/idea* " 

  # vagrant ssh 
  # login using vagrant/vagrant
  # startx  #to run ubuntu gui desktop
  # spring init --list  #to show springboot initializer options
end
