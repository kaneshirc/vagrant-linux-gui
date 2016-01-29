# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # config.vm.box = "ubuntu/trusty64"
  config.vm.box = "debian/jessie64"

  # config.vm.box_check_update = false

  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.cpus = 2
    vb.memory = "8192"
  end

  config.vm.provision "shell", inline: <<-SHELL

    # Update repository from Japan.
    sudo mv /etc/apt/sources.list /etc/apt/sources.list.bak.`date "+%Y%m%d_%H%M%S"`
    sudo cp /vagrant/sources.list /etc/apt/sources.list
    sudo apt-get update
    sudo apt-get -y upgrade

    # Install desktop.
    sudo apt-get install -y lxde

    # Change language settings to Japanese.
    sudo sed -i.bak -e "s/# ja_JP.UTF-8/ja_JP.UTF-8/g" /etc/locale.gen
    sudo locale-gen
    sudo update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
    source /etc/default/locale
    echo $LANG
  SHELL
end
