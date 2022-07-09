VAGRANT_API_VERSION = "2"
VM_NAME="devstack"

Vagrant.configure(VAGRANT_API_VERSION ) do |config|

    config.vm.define "devstack"
    config.vm.box = "focal-server-cloudimg-amd64-vagrant"
    config.vm.box_url = "https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64-vagrant.box"

    config.vm.network "private_network", ip: "192.168.56.10", nic_type: "virtio"
  
    config.vm.provider "virtualbox" do |v|
      v.name = "devstack"
      v.cpus = 4 # <--- Devstack requires at least 2 vCPU
      v.memory = 8192 # <--- Devstack requires at least 4 GB of RAM
  
      # Enable nested virtualization, so it will be possible to run VMs inside your VM
      v.customize ["modifyvm", :id, "--nested-hw-virt", "on"]
      # Enable promiscuous mode for the network interface number "2"
      v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    end
  
    # Enable provisioning with Ansible
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "devstack.yml"
    end
  end