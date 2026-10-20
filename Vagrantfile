# -*- mode: ruby -*-
# vi: set ft=ruby :
#
# Vagrant configuration file
#
# References:
#
# * Vagrantfile | Vagrant | HashiCorp Developer
#   https://developer.hashicorp.com/vagrant/docs/vagrantfile
#
# This work is based on "The common Vagrantfile templates" project:
# https://gitlab.com/the-common/vagrantfile-templates
#
# Copyright 2025 林博仁(Buo-ren Lin) <buo.ren.lin@gmail.com>
# SPDX-License-Identifier: AGPL-3.0-or-later

Vagrant.configure("2") do |config|
  # Get the directory name containing this Vagrantfile to use as VM name prefix
  project_name = File.basename(Dir.pwd)

  # Find more Vagrant boxes at:
  # https://portal.cloud.hashicorp.com/vagrant/discover?architectures=amd64&providers=virtualbox&query=bento
  config.vm.box = "bento/debian-13"

  # Configure synced folders for ease access to project files
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider :virtualbox do |v|
    v.cpus = 2
    v.memory = 512

    # Use Virt-IO network adapter to improve networking performance
    v.default_nic_type = "virtio"
  end

  config.vm.define "CA server" do |ca_server|
    ca_server.vm.hostname = "server"
    ca_server.vm.network "private_network", ip: "192.168.56.191"

    ca_server.vm.provider :virtualbox do |v|
      v.name = "#{project_name} - CA server"
    end
  end

  config.vm.define "server", autostart: false do |server|
    server.vm.hostname = "server"
    server.vm.network "private_network", ip: "192.168.56.192"

    server.vm.provider :virtualbox do |v|
      v.name = "#{project_name} - Emulated TLS server"
    end
  end

  config.vm.define "client", autostart: false do |client|
    client.vm.hostname = "client"
    client.vm.network "private_network", ip: "192.168.56.193"

    client.vm.provider :virtualbox do |v|
      v.name = "#{project_name} - Emulated TLS client"
    end
  end
end
