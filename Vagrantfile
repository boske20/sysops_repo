# -*- mode: ruby -*-
# vi: set ft=ruby :
servers=[
#  {
#    :hostname => "web02",
#    :ip => "192.168.33.21",
#    :box => "centos/8",
#    :ram => 2048,
#    :cpu => 1,
#    :guest => 80,
#    :host => 8080,
#    :host_ip => "127.0.0.1"
#  },
#  {
#    :hostname => "web01",
#    :ip => "192.168.33.20",
#    :box => "ubuntu/bionic64",
#    :ram => 2048,
#    :cpu => 1,
#    :guest => 80,
#    :host => 8081,
#    :host_ip => "127.0.0.1"
#  },
  {
    :hostname => "prestashop01.local",
    :ip => "192.168.33.42",
    :box => "centos/8",
    :ram => 2048,
    :cpu => 1,
    :guest => 80,
    :host => 8095,
    :host_ip => "127.0.0.1"
  }
]
Vagrant.configure(2) do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network "private_network", ip: machine[:ip]
            node.vm.network "forwarded_port", guest: machine[:guest], host: machine[:host], host_ip: machine[:host_ip]
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
             end
         end
        config.vm.provision "shell", inline: <<-SHELL
           sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config    
           systemctl restart sshd.service
     SHELL
  end
end
