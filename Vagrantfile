# -*- mode: ruby -*-
# vi: set ft=ruby :
# RR

Vagrant.configure(2) do |config|
    
config.vm.define "pxeserver" do |pxeserver|
        pxeserver.vm.box = 'centos/7'
        pxeserver.vm.host_name = 'pxeserver'
        pxeserver.vm.network :private_network, ip: '10.0.0.20', virtualbox_intnet: 'pxenet'
        pxeserver.vm.provider :virtualbox do |vb|
         vb.customize ['modifyvm', :id, '--memory', '2024']
         vb.customize ['modifyvm', :id, '--cpus', '1']
        pxeserver.vm.provision "shell",
            name: "Setup PXE server",
            path: "setup_pxe.sh"
        end
    end



    config.vm.define "pxeclient" do |pxeclient|
        pxeclient.vm.box = 'centos/7'
        pxeclient.vm.host_name = 'pxeclient'
        pxeclient.vm.network :private_network, ip: "10.0.0.21"
        pxeclient.vm.provider :virtualbox do |vb|
         vb.customize ['modifyvm', :id, '--boot1', 'net']
         vb.customize ['modifyvm', :id, '--boot2', 'none']
         vb.customize ['modifyvm', :id, '--boot3', 'none']
         vb.customize ['modifyvm', :id, '--boot4', 'none']
         vb.customize ['modifyvm', :id, '--biospxedebug', 'on']
         vb.customize ['modifyvm', :id, '--cableconnected2', 'on']
         vb.customize ['modifyvm', :id, '--nicbootprio2', '1']
         vb.customize ['modifyvm', :id, "--nictype2", '82540EM']
         vb.customize ["modifyvm", :id, "--memory", "4096"]
         vb.customize ["modifyvm", :id, "--cpus", "1"]
        end
    end
end
