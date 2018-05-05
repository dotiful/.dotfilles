# -*- mode: ruby -*-
# vi: set ft=ruby :

# required_plugins = %w( vagrant-parallels vagrant-auto_network vagrant-hostmanager )
# required_plugins.each do |plugin|
#   exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
# end

Vagrant.configure("2") do |config|
  config.vm.box = "monsenso/macos-10.13"

  # Disable automatic box update checking.
  config.vm.box_check_update = false

  # Create a private network
  config.vm.network :private_network, :auto_network => true
  # config.vm.network "forwarded_port", guest: 8080, host: 8080

  # Share an additional folder to the guest VM via Network Shared Folder.
  # config.vm.synced_folder ".", "/vagrant", :disabled => true
  # config.vm.synced_folder ".", "/vagrant", id: "vagrant"
  config.vm.synced_folder ".", "/vagrant", type: "nfs" # or "rsync"
  # config.vm.synced_folder "./dotfiles", "/Users/vagrant/freckles",
  #   id: "vagrant",
  #   :nfs => true,
  #   :mount_options => ['nolock,vers=3,udp,noatime,actimeo=1,resvport'],
  #   :export_options => ['async,insecure,no_subtree_check,no_acl,no_root_squash']

  # config.vm.synced_folder "/usr/local/Homebrew", "/usr/local/Homebrew",
  #   id: "shared",
  #   :nfs => true,
  #   :mount_options => ['nolock,vers=3,udp,noatime,actimeo=1,resvport'],
  #   :export_options => ['async,insecure,no_subtree_check,no_acl,no_root_squash']

  config.vm.provider 'virtualbox' do |vb|
    vb.linked_clone = true
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = false
    # Customize the amount of memory on the VM:
    vb.memory = "4096"
  end

  # config.vm.provision "shell", inline: <<-SHELL
  #   curl https://freckles.io | bash -s -- freckelize -v /vagrant/vagrant.vars.freckle -f /vagrant
  # SHELL

  # Enable provisioning with a shell script.
  # config.vm.provision "shell", inline: <<-SHELL
  #   if [ ! -d /usr/local/Homebrew ]; then
  #   	echo " [ == ] Installing Homebrew ... [ <== ]"
  #   	curl -fsSL https://raw.github.com/rcmdnk/homebrew-file/install/install.sh | sh
  #   fi
  # SHELL

  # Vagrant.local
  #
  # Use this to insert your own (and possibly rewrite) Vagrant config lines.
  # If a file 'Vagrant.local' exists in the same directory as this Vagrantfile,
  # it will be evaluated as ruby inline as it loads.
  # if File.exist?(File.join(vagrant_dir, 'Vagrant.local'))
  #   eval(IO.read(File.join(vagrant_dir, 'Vagrant.local')), binding)
  # end
end
