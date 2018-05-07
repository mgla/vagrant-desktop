# -*- mode: ruby -*-

VAGRANTFILE_API_VERSION = "2"
VAGRANT_DEFAULT_PROVIDER = "virtualbox"

hostname_prefix = 'local01-'
domain = 'local'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # https://github.com/dotless-de/vagrant-vbguest
  config.vbguest.auto_update = true
  config.vm.define "linuxgui" do |master|
    master.vm.box      = "debian/contrib-jessie64"
    master.vm.box_url  = "https://atlas.hashicorp.com/debian/contrib-jessie64"
    master.vm.hostname = "#{hostname_prefix}-linuxgui.#{domain}"
    master.vm.network    "private_network", ip: "192.168.33.10"
    master.vm.network    "forwarded_port", guest: 8000, host: 8000
    master.vm.synced_folder ".", "/home/vagrant/vagrant-desktop", create: true
    master.vm.synced_folder "~", "/home/vagrant/host-home", create: true
    # Settings for VirtualBox
    master.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.customize ["modifyvm", :id,
        "--memory", "4096",
        "--vram", "32",
        "--cpus", "2",
        "--ioapic", "on"
      ]
    end
    master.vm.provision :hosts, :sync_hosts => true
    master.vm.provision "shell", path:   "vagrant/system-prep.sh"
    # Configure vagrant user environment as vagrant user.
    master.vm.provision "shell", privileged: false, path:   "vagrant/user-config.sh"
    master.vm.provision "shell", path:   "vagrant/vbox-config.sh"
    master.vm.provision "shell", inline: "/bin/systemctl start lightdm"
  end

end

# vi: set ft=ruby :
