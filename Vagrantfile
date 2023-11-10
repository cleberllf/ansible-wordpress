# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "wordpress" => {"memory" => "1024", "cpu" => "1", "clone" => "true", "ipA" => "251", "ipB" => "251", "image" => "ubuntu/jammy64"},
  #"wordpress_bd" => {"memory" => "1024", "cpu" => "1", "clone" => "true", "ipA" => "252", "ipB" => "252", "image" => "ubuntu/jammy64"},
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "192.168.0.#{conf["ipA"]}"
      machine.vm.network "public_network", ip: "172.16.0.#{conf["ipB"]}"
      #machine.vm.network "forwarded_port", guest: 22, host: 2222
#      machine.vm.network "public_network", ip: "172.16.0.#{conf["ipB"]}", bridge: "eno1"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.linked_clone = conf["clone"]
      end
      #machine.vm.provision "shell", path: "shell_script.sh"
    end
  end
end