# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?('dotenv')
  raise <<~ERROR
    "dotenv" is not installed!
    Please execute the below command to install plugins.
    - $ vagrant plugin install dotenv
  ERROR
end

unless Vagrant.has_plugin?('vagrant-vbguest')
  raise <<~ERROR
    "vagrant-vbguest" is not installed!
    Please execute the below command to install plugins.
    - $ vagrant plugin install vagrant-vbguest
  ERROR
end

$provision = <<-'SCRIPT'

  apt-get update

  # install dev tools
  apt-get install -y git
  apt-get install -y curl
  apt-get install -y unzip
  apt-get install -y build-essential autoconf libtool
  apt-get install -y libgflags-dev libgtest-dev
  apt-get install -y clang libc++-dev
  apt-get install -y tmux

  ################################################################################
  # install docker
  ################################################################################

  # ref. https://docs.docker.com/engine/installation/linux/docker-ce/debian/
  apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common -y

  curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
  # apt-key fingerprint 0EBFCD88

  add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
     $(lsb_release -cs) \
     stable"

  apt-get update

  apt-get install docker-ce -y

  ################################################################################
  # install docker compose
  ################################################################################

  curl -sL https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

  chmod +x /usr/local/bin/docker-compose

SCRIPT

$start = <<-'SCRIPT'

  # make node_modules folder
  # mkdir -p $REPO_ROOT/frontend/client/node_modules
  # chown -R vagrant:vagrant $REPO_ROOT/frontend/client/node_modules
  # mount --bind $HOME/node_modules $REPO_ROOT/frontend/client/node_modules

SCRIPT

Dotenv.load

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  # config.disksize.size = '20GB'

  config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
  end

  # Network settings
  config.vm.network "private_network", ip: "192.168.33.10"

  # Synced folder settings
  config.vm.synced_folder "./", "/vagrant", type: "virtualbox" , mount_options: ['dmode=777', 'fmode=777']

  # Provisioning
  config.vm.provision :shell, inline: $provision

  # Provisioning always
  config.vm.provision :shell, inline: $start, run: 'always'

end
