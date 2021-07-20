# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    vb.name = "my_vm"

    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end
  config.vm.provision "shell", inline: <<-SHELL
    yum -y install git rpm rpm-build vim java-1.8.0-openjdk-devel wget
    wget http://www.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
    tar -xvzf apache-maven-3.3.9-bin.tar.gz
    #Add Maven to PATH
    echo export PATH=/home/vagrant/apache-maven-3.3.9/bin:\$PATH >> /home/vagrant/.bashrc
   
    # SELinux Permissive
    setenforce 0
    # set timezone JST
    timedatectl set-timezone Europe/Rome
    # EPEL
    yum install -y epel-release
    yum install -y vim git

    # install docker
    yum remove docker \
    docker-client \
    docker-client-latest \
    docker-common \
    docker-latest \
    docker-latest-logrotate \
    docker-logrotate \
    docker-selinux \
    docker-engine-selinux \
    docker-engine
    yum install -y yum-utils \
    device-mapper-persistent-data \
    lvm2

    yum install -y policycoreutils-python libcgroup
    rpm -i https://mirrors.aliyun.com/docker-engine/yum/repo/main/centos/7/Packages/docker-engine-selinux-1.12.1-1.el7.centos.noarch.rpm
    rpm -i https://mirrors.aliyun.com/docker-engine/yum/repo/main/centos/7/Packages/docker-engine-1.12.1-1.el7.centos.x86_64.rpm

    # vagrant user add docker group
    gpasswd -a vagrant docker
    # docker running
    systemctl enable docker
    systemctl start docker
  SHELL
end
