# -*- mode: ruby -*-
# vi: set ft=ruby :

API_VERSION = "2"
BOX_NAME = "centos/7"
BOX_IP = "192.168.56.3"
DOMAIN = "nip.io"
PRIVATE_KEY = "~/.ssh/id_rsa"
PUBLIC_KEY = '~/.ssh/id_rsa.pub'

Vagrant.configure("2") do |config|
    # The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at
    # https://docs.vagrantup.com.
  
    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://atlas.hashicorp.com/search.
        
    ################ VBox #############################
    # let's use vbox
    config.vm.define "jenkins_box" do |jenkins|
        config.vm.box = BOX_NAME
        config.vm.host_name = BOX_IP + '.' + DOMAIN
        config.ssh.insert_key = false
        config.ssh.private_key_path = [PRIVATE_KEY, "~/.vagrant.d/insecure_private_key"]
        config.vm.provision "file", source: PUBLIC_KEY, destination: "~/.ssh/authorized_keys"        
        jenkins.vm.network :private_network, ip: "192.168.56.3"
        jenkins.vm.provider :virtualbox do |v|
           v.gui = false
           v.memory = 2048
        end
    end      
     
    config.vm.provider "virtualbox" do |v|
        v.memory = "2024"
        v.cpus = "2"
    end

    if Vagrant.has_plugin?("vagrant-hostmanager")
        config.hostmanager.enabled = true
        config.hostmanager.manage_host = true
        config.hostmanager.manage_guest = true
    end
  end