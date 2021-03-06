###
# @package  breed
# @author   Walker de Alencar <@walkeralencar>
# @author   Roberto L. Machado <@robmachado>
##
Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  ## need to change $HOSTNAME in './config" if you change here
  config.vm.hostname = "breed.vm"

  ## Configure cached packages to be shared between instances of the same base box.
  ## More info on http://fgrehm.viewdocs.io/vagrant-cachier/usage
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
    config.cache.auto_detect = false
    config.cache.enable :apt
  end

  ## Change between private or public access to you machine.
  config.vm.network "private_network", ip: "192.168.50.10"
  config.vm.network "public_network"

  ## Site specific data to be served by the system
  ## http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/srv.html
  config.vm.synced_folder "./srv", "/srv"

  config.vm.provider "virtualbox" do |v|
      v.name = "breed"
  end

  config.vm.provision "shell", inline: 'echo \'LC_ALL="en_US.UTF-8"\' > /etc/default/locale'

  ## Fix tty msg error by @robmachado
  config.vm.provision "fix-no-tty", type: "shell" do |s|
      s.privileged = false
      s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  config.vm.provision :shell, path: "provision/setup.sh"
end
