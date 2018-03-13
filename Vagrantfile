# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
    config.vm.define :LoadBalancer do |node1|
    node1.vm.box = "centos1706_v0.3.0"
    node1.vm.network :private_network, ip: "192.168.33.12"
    node1.vm.provider :virtualbox do |vb1|
      vb1.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "LoadBalancer" ]
    end
    config.vm.provision "chef_solo" do |chef|
       chef.cookbooks_path = "cookbooks"
       chef.add_recipe "loadbalancer"
       chef.json = {
        "web_servers" => [
          {"ip":"192.168.33.13"},{"ip":"192.168.33.14"}
         ]
       }
    end
  end


  config.vm.define :server1 do |node2|
    node2.vm.box = "centos1706_v0.3.0"
    node2.vm.network :private_network, ip: "192.168.33.13"
    node2.vm.provider :virtualbox do |vb2|
      vb2.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "server1" ]
    end
    config.vm.provision "chef_solo" do |chef|
       chef.cookbooks_path = "cookbooks"
       chef.add_recipe "httpd"
       chef.json = {
         	"servidor" => "Servidor 1",
	       "ip" => "192.168.33.13"
		   }
    end
  end

 config.vm.define :server2 do |node3|
    node3.vm.box = "centos1706_v0.3.0"
    node3.vm.network :private_network, ip: "192.168.33.14"
    node3.vm.provider :virtualbox do |vb3|
      vb3.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "server2" ]
    end
    config.vm.provision "chef_solo" do |chef|
       chef.cookbooks_path = "cookbooks"
       chef.add_recipe "httpd"
       chef.json = {
         "servidor" => "Servidor 2",
         "ip" => "192.168.33.14"
       }
    end
  end
end
