# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

 config.hostmanager.enabled = true
 config.hostmanager.ignore_private_ip = false
 config.hostmanager.include_offline = true
 config.vm.boot_timeout = 600


 config.vm.define "puppet" do |puppet|
    # Puppetmaster on Centos7
    config.vm.provider "virtualbox" do |v|
      v.memory =2048
    end
    puppet.vm.synced_folder ".", "/vagrant"
    puppet.vm.synced_folder "../code", "/puppet_code"
    puppet.vm.synced_folder "../puppetserver", "/puppet_puppetserver"
    puppet.vm.box = "doozr/centos7"
    puppet.vm.hostname = "puppet.unixolu.com"
    puppet.vm.network :private_network, ip: "10.0.0.10"
    puppet.hostmanager.aliases = %w(puppet)
    puppet.vm.provision "shell", inline: <<-SHELL
      sudo yum update -y
      sudo rpm -ivh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm
      sudo yum install puppetserver -y
      sudo rm -rf /etc/puppetlabs/code
      sudo ln -s /puppet_code /etc/puppetlabs/code
      sudo rm -rf /etc/puppetlabs/puppetserver
      sudo ln -s /puppet_puppetserver /etc/puppetlabs/puppetserver
      sudo sed -i 's/2g/512m/g' /etc/sysconfig/puppetserver
      sudo service puppetmaster start
      echo "*.unixolu.com" | sudo tee /etc/puppetlabs/puppet/autosign.conf
    SHELL
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
