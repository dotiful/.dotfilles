# -*- mode: ruby -*-
# vi: set ft=ruby :

required_plugins = %w( vagrant-ssh-config-cache vagrant-auto_network )
required_plugins.each do |plugin|
  exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

Vagrant.configure("2") do |config|
  config.vm.box = "monsenso/macos-10.13"

  # Disable automatic box update checking.
  config.vm.box_check_update = false

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"

  # Create a private network
  config.vm.network :private_network, :auto_network => true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # Use NFS for the shared folder

  # config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.vm.synced_folder "./tmp", "/vagrant", id: "vagrant", type: "rsync", owner: "vagrant", group: "admin"
  config.vm.synced_folder "./dotfiles/", "/Users/vagrant/freckles", id: "freckles", type: "nfs"
  # config.vm.synced_folder "./dotfiles/", "/Users/vagrant/freckles", id: "freckles", type: "rsync", owner: "vagrant", group: "admin", rsync__exclude: [".git", ".vagrant", ".vscode"]

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # See https://www.virtualbox.org/manual/ch08.html for possible options.
  config.vm.provider 'virtualbox' do |vb|
    vb.linked_clone = true
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
    # Customize the amount of memory on the VM:
    vb.memory = "4096"
    # Enable 3D Display Acceleration
    vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
    # Enable bidirectional clipboard
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
  end

  # config.vm.provision "shell", inline: <<-SHELL
  #   curl https://freckles.io | bash -s -- freckelize -v /vagrant/vagrant.vars.freckle -f /vagrant
  # SHELL
end
