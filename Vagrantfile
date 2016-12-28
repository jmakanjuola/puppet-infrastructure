# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

 config.hostmanager.enabled = true
 config.hostmanager.ignore_private_ip = false
 config.hostmanager.include_offline = true 

 
 config.vm.define "puppet" do |puppet|
    # Puppetmaster on Centos7
    puppet.vm.box = "centos/7"
    puppet.vm.hostname = "puppet.unixolu.com"
    puppet.vm.network :private_network, ip: "10.0.0.10"
    puppet.hostmanager.aliases = %w(puppet) 
  end

  config.vm.define "agent1" do |agent1|
    # Puppet agent on Centos 7
    agent1.vm.box = "centos/7"
    agent1.vm.hostname = "agent1.unixolu.com"
    agent1.vm.network :private_network, ip: "10.0.0.11"
    agent1.hostmanager.aliases = %w(agent1) 
  end
  
  config.vm.define "agent2" do |agent2|
    # Puppet agent on Debian
    agent2.vm.box = "ARTACK/debian-jessie"
    agent2.vm.hostname = "agent2.unixolu.com"
    agent2.vm.network :private_network, ip: "10.0.0.12"
    agent2.hostmanager.aliases = %w(agent2) 
  end
end
