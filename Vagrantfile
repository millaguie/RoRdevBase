# -*- mode: ruby -*-
# vi: set ft=ruby :
unless Vagrant.has_plugin?("vagrant-vbguest")
  raise "Please install the vagrant-vbguest plugin by running `vagrant plugin install vagrant-vbguest`"
end

VAGRANTFILE_API_VERSION = "2"

# Change this values to meet your host needs
MEMORY =  2048
CPU_COUNT = 2

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Let's use debian, It's the same version as in the server
  config.vm.box = "debian/wheezy64"
  system_chef_solo = '/opt/chef/bin/chef-solo'
  # Workaround for tty issue
  config.vm.provision "shell",
    inline: "if `grep 'tty..s .. mesg n' /root/.profile `; then echo 'Profile allready pached' ; else echo 'tty -s && mesg n' >> /root/.profile; fi"
  # Now install rvm, and some related stuff (this takes soooo long, so grab a coffe)
  config.vm.provision :shell, inline: "echo Installing tough stuff, it\\'s gonna take long, grab a coffe and relax"
  config.vm.provision :shell, inline: "apt-get update ; apt-get -y upgrade"
  config.vm.provision :shell, path: "install-rvm.sh", args: "stable", privileged: false
  config.vm.provision :shell, path: "install-ruby.sh", args: "1.9.3 rails bundler", privileged: false
  # do you need extra ruby versions?
  #config.vm.provision :shell, path: "install-ruby.sh", args: "2.0.0 rails haml", privileged: false  # Configurate the virtual machine to use 2GB of RAM
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", MEMORY.to_s]
    vb.customize ["modifyvm", :id, "--cpus", CPU_COUNT.to_s]
    config.vm.post_up_message = "OK, now remember some useful commands:\nvagrant ssh (to get into the development machine)\ncd /vagrant (to get into the source code)\nYou can check your rails server at your own http://localhost:3000\n.. and work .. "
  end

  # Forward the Rails server default port to the host
  config.vm.network :forwarded_port, guest: 3000, host: 3000

  # Use Chef Solo to provision configurations in our virtual machine
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]

    chef.add_recipe "apt"
    chef.add_recipe "vim"
    chef.add_recipe "mysql::server"
    chef.add_recipe "mysql::client"

    chef.json = {
      # MySQL configuration, a blank one, 
      mysql: {
        server_root_password: '',
        server_debian_password: ''
      }
    }
  end
end
