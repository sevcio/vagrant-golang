# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.box = "precise64"
  config.vm.network :bridged, :bridge => "eth0"
  config.vm.forward_port 80, 8080
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.provision :puppet do |puppet|
    puppet.module_path      = "modules"
    puppet.manifests_path  = "manifests"
    puppet.manifest_file      = "init.pp"
    #puppet.options << '--verbose'
    #puppet.options << '--debug'
  end
end

Vagrant.configure("2") do |config|
  # other config here
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--nictype1", "virtio"]
    v.customize ["modifyvm", :id, "--nictype2", "virtio"]
    v.customize ["modifyvm", :id, "--nictype3", "virtio"]
    v.customize ["modifyvm", :id, "--memory", 2048]
    v.customize ["modifyvm", :id, "--name", "VagrantMachine"]
  end  
  config.vm.synced_folder ".", "/home/vagrant/go/src/#{File.basename(Dir.getwd)}"
end
