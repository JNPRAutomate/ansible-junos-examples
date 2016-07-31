# ansible-junos-examples

Project to demonstrate Ansible modules for Junos

In this project you'll find:
- Examples of playbooks for various Ansible modules for Junos:
  - **core - junos_config**: add config, delete config, rollback
  - **core - junos_facts**: collect facts, collect configuration in XML, TEXT or JSON
  - **core - junos_command**: execute cli commands or RPC on devices
  - **core - junos_template**: deploy configuration templates on device
- Vagrant file to start a virtual topology with 2 vSRX

# Installation instructions

A virtual topology based on Vagrant and vSRX is provided to help everyone to get started.

#### Install Vagrant and Vagrant plugin for Junos

Vagrant [installation instructions](https://www.vagrantup.com/docs/installation/)
Vagrant plugin installation
```
vagrant plugin add vagrant-junos
```

Once Vagrant is installed, you can start the topology
```
git clone https://github.com/JNPRAutomate/ansible-junos-examples.git
cd ansible-junos-examples
vagrant up
```

2 devices will be started (vsrx1 & vsrx2). Both devices are connected back to back with 2 interfaces.
```
ge-0/0/0|                   ge-0/0/0|    
=============               =============
|           | ge-0/0/[1-2]  |           |
|   vsrx1   | ------------- |   vsrx2   |
|           | ------------- |           |
=============               =============
```

You can connect to both VM in SSH
```
vagrant ssh vsrx1
vagrant ssh vsrx2
```

# Ansible Core - Examples of playbooks
All playbooks are located in the directory `playbook-core/`

## junos_config
[Official documentation](https://docs.ansible.com/ansible/junos_config_module.html) on Ansible Website
### Add configuration lines on device
##### Change the hostname of the device
```
ansible-playbook playbook-core/pb.config.update_hostname.yaml
```
> this operation is idempotent, if executed twice, Ansible will not report change the second time.

##### Add description on multiple interfaces using a list as input
```
ansible-playbook playbook-core/pb.config.add_description.yaml
```
### Delete configuration lines on devices
```
ansible-playbook playbook-core/pb.config.delete_description.yaml
```

### Rollback configuration
```
ansible-playbook playbook-core/pb.config.rollback.yaml
```

## junos_command
[Official documentation](https://docs.ansible.com/ansible/junos_command_module.html) on Ansible Website

### Execute show system user and get response in JSON & XML
```
ansible-playbook playbook-core/pb.command.show_version.yaml
```

### Query interface status and validate response with wait_for
```
ansible-playbook playbook-core/pb.command.show_interface.yaml
```

### Use previous command output to only query interfaces status if interfaces are UP
```
ansible-playbook playbook-core/pb.command.show_ext_if_up.yaml
```

## junos_facts
[Official documentation](https://docs.ansible.com/ansible/junos_facts_module.html) on Ansible Website

### Query facts and configuration in XML format on device
The configuration will be automatically converted from XML to JSON
```
ansible-playbook playbook-core/pb.facts.get_config_json_xml.yaml
```

### Query configuration in TEXT and save to a file
```
ansible-playbook playbook-core/pb.facts.get_config_txt.yaml
```

## junos_template
[Official documentation](https://docs.ansible.com/ansible/junos_template_module.html) on Ansible Website
### Generate a snippet of configuration based on a jinja2 template and deploy to device
```
ansible-playbook playbook-core/pb.template.push_interface.yaml
```

## junos_package
[Official documentation](https://docs.ansible.com/ansible/junos_package_module.html) on Ansible Website.  
Example not available yet

## junos_netconf
[Official documentation](https://docs.ansible.com/ansible/junos_netconf_module.html) on Ansible Website.  
Example not available yet

# Ansible Galaxy - Examples of playbooks

## junos_jsnapy
### Execute multiple tests define with jsnapy 
```
ansible-playbook playbook-galaxy/pb.jsnapy.test_pass.yaml
```

## junos_get_config
Example not available yet

## junos_get_facts
Example not available yet

## junos_get_table
Example not available yet

## junos_install_config
Example not available yet

## junos_install_os
Example not available yet

## junos_ping
Example not available yet

## junos_cli
Example not available yet

## junos_rpc
Example not available yet

## junos_zeroize
Example not available yet

## junos_srx_cluster
Example not available yet

## junos_shutdown
Example not available yet

## junos_rollback
Example not available yet
