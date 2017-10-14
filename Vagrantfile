Vagrant.configure("2") do |config|
#  Vagrant.require_version ">= 2.0.0

  config.vm.box = "ubuntu/trusty64"		# Default box for this project
  config.vm.box_check_update = false		# Auto-updates disabled
  #config.vm.box_download_checksum
  #config.vm.box_download_checksum_type		# "md5", "sha1", and "sha256"
  #config.vm.box_download_client_cert
  #config.vm.box_download_ca_cert
  #config.vm.box_download_insecure		# If true, then SSL certificates from the server will not be verified.
  #config.vm.box_download_location_trusted       # If true, then all HTTP redirects will be treated as trusted. 
  #config.vm.box_url				# The URLs can also be local files by using the file:// scheme. For example: "file:///tmp/test.box"
  #config.vm.box_version
  #config.vm.communicator
  #config.vm.graceful_halt_timeout 		#  Defaults to 60 seconds.
  #config.vm.guest				# This defaults to :linux
  #config.vm.hostname 				# The hostname the machine should have
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  #config.vm.post_up_message 			# A message to show after vagrant up. 
  #config.vm.provider
  #config.vm.provision
  #config.vm.synced_folder 
  #config.vm.usable_port_range 			# A range of ports Vagrant can use for handling port collisions and such. Defaults to 2200..2250
 
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "qemu"
    libvirt.host = "localhost"
    libvirt.uri = "qemu:///system"
    #libvirt.connect_via_ssh = true
    #libvirt.username = root
  end

  # Loadbalancer 
  config.vm.define :lb01, primary: true, autostart: true do |lb01|
    lb01.vm.hostname = "anax-lb01"
    lb01.vm.network "private_network", ip: "10.0.0.10"
    lb01.vm.synced_folder "../src", "/vagrant_data/src", create: true, type: "rsync", rsync__args: ["--verbose", "--archive", "--delete", "-z", "--copy-links"], rsync__exclude: [".git/",".vagrant","Vagrantfile","vagrant-notes.txt"],rsync__verbose: true
  end

  # Loadbalancer 
  config.vm.define :lb02, autostart: true do |lb02|
    lb02.vm.hostname = "anax-lb02"
    lb02.vm.network "private_network", ip: "10.0.0.11"
    lb02.vm.synced_folder "../src", "/vagrant_data/src", create: true, type: "rsync", rsync__args: ["--verbose", "--archive", "--delete", "-z", "--copy-links"], rsync__exclude: [".git/",".vagrant","Vagrantfile","vagrant-notes.txt"],rsync__verbose: true
  end

end
