# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # config.vm.box = "centos/7"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../shared", "/opt/shared"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  N = 3
  (1..N).each do |machine_no|
    config.vm.define "centos7-vagrant#{machine_no}" do |centos7|
      centos7.vm.box = "centos/7"
      centos7.vagrant.plugins = ["vagrant-vbguest"]
      centos7.ssh.forward_agent = true
      #comment below line to not insert key in base vm
      #centos7.ssh.insert_key = false
      centos7.vm.network "private_network", ip: "192.168.56.#{10+machine_no}"
      centos7.vm.network "forwarded_port", guest: 22, host: "#{2220+machine_no}", id: "ssh"
      if machine_no == 1
        centos7.vm.hostname = "sun"
      end
      if machine_no == 2
        centos7.vm.hostname = "earth"
      end
      if machine_no == 3
        centos7.vm.hostname = "venus"
      end
      centos7.vm.provider "virtualbox" do |vb|
        vb.memory = 4096
        vb.cpus = 2
        vb.name = "centos7-vagrant#{machine_no}"
      end
      centos7.vm.provision "shell", inline: <<-SHELL
        useradd -m -U monkey
        echo monkey ALL=NOPASSWD:ALL > /etc/sudoers.d/monkey && chmod 440 /etc/sudoers.d/monkey
        mkdir -m 700 /home/monkey/.ssh
        echo 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAzXxUsfUYKARKhduUhJsbpjLtttwwRl5xwfwN5Gh+byR5mJn76DoTKLX7P4K1qNeHpMBCqFnBUvKOsKw9aIqXEG1Iekw/GPExbrmpi9/Cz32O+g3RcP+Mp45bZnio+h64T26jQ8+kElLxnlAU4gIi6ZKjADUBiY3nOmq2WsofcIBWpXBanHFTbpUtx0qoWqlPwXhqFNIP9TaZDoNN3AIVX7/pL+YqGZluMyQ1Hpbmpdp5j/rgZO6zJkBvdmjsZhXsB+bQWrZvZplgO0OFCHvZtCUdUbi8eQBbv7DZrURZfcEgqETAaYVDK9xZQicatiFbrTkJjcD1TRaqsLYe7xfUxw== monkey@controller' >> /home/monkey/.ssh/authorized_keys
        chmod 600 /home/monkey/.ssh/authorized_keys
        chown -R monkey:monkey /home/monkey/.ssh
      SHELL
    end
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
