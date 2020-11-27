# Loading configuration file
require 'yaml'
servers = YAML.load_file('hosts.yml')
total_hosts = servers.length

Vagrant.configure("2") do |config|

# Setup of webserver and loadbalancer nodes
    servers.each_with_index do |server, index|
        config.vm.define server["name"] do |srv|
            srv.vm.box = server["box"]
            srv.vm.hostname = server["name"]
            srv.vm.network "private_network", ip: server["ip"]
            srv.vm.provider "virtualbox" do |vb|
                vb.name = server["name"]
                vb.memory = server["ram"]
            end

# Provisioning nodes with Ansible when all of them are setup
            if index == total_hosts - 1
                config.vm.provision "ansible" do |ansible|
                    ansible.playbook = "provisioning/nginx.yml"
                    ansible.limit = "all"
                    ansible.groups = {
                        "loadbalancers" => ["loadbalancer"],
                        "webservers" => ["web1", "web2"],
                        "all_groups:children" => ["loadbalancers", "webservers"]
                        }
                end
            end
        end
    end
end
