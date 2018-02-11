# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |vb, override|
    vb.memory = "1024"

    override.vm.box = "bento/ubuntu-16.04"
    override.vm.network "forwarded_port", guest: 80, host: 8080

    if ENV["VAGRANT_NETWORK_BRIDGE"]
      override.vm.network "public_network", bridge: ENV["VAGRANT_NETWORK_BRIDGE"]
    end
  end

  config.vm.provision "docker" do |d|
    d.build_image "/vagrant", args: "-t devdocs"
    d.run "devdocs", args: "--publish 0.0.0.0:80:9292 --restart unless-stopped"
  end
end
