# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  (1..2).each do |id|
    re_name  = ( "vsrx" + id.to_s ).to_sym

    config.vm.define re_name do |vsrx|
      vsrx.vm.box = "juniper/ffp-12.1X47-D20.7-packetmode"
      vsrx.vm.network "private_network",
         ip: "192.168.1.#{id}",
         virtualbox__intnet: "neta",
         nic_type: 'virtio'
       vsrx.vm.network "private_network",
         ip: "192.168.2.#{id}",
         virtualbox__intnet: "netb",
         nic_type: 'virtio'
    end
  end

  ##############################
  ## Box provisioning    #######
  ##############################
  if !Vagrant::Util::Platform.windows?
      config.vm.provision "ansible" do |ansible|
          ansible.groups = {
              "all" => ["vsrx1", "vsrx2"]
          }
          ansible.playbook = "playbook-core/pb.command.show_version.yaml"
      end
  end
end
