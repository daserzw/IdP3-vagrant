# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_ansible = <<SCRIPT
apt-get -y install software-properties-common
apt-add-repository ppa:ansible/ansible
apt-get -y update
apt-get -y install ansible
apt-get -y install git

SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty32'
  config.vm.hostname = 'idp'
  config.vm.provision 'shell', inline: $install_ansible
  # Patch for https://github.com/mitchellh/vagrant/issues/6793
  config.vm.provision "shell" do |s|
    s.inline = '[[ ! -f $1 ]] || grep -F -q "$2" $1 || sed -i "/__main__/a \\    $2" $1'
    s.args = ['/usr/bin/ansible-galaxy', "if sys.argv == ['/usr/bin/ansible-galaxy', '--help']: sys.argv.insert(1, 'info')"]
  end
  config.vm.network "private_network", ip: "10.0.3.2"
  config.vm.network "private_network", ip: "10.0.4.2"
end
