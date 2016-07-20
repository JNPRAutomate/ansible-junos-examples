# ansible-core-junos-examples

Project to demonstrate new Core module for Junos in Ansible 2.1+
In this project you'll find:
- examples of playbooks for:
  - junos_config: add config, delete config, rollback)
  - junos_facts: collect facts, collect configuration in XML, TEXT or JSON)
  - junos_command: execute cli commands or RPC on devices)
  - junos_template: deploy configuration templates on device.
- Vagrant file to start a virtual topology with 2 vSRX

# Virtual topology

A virtual topology based on Vagrant and vSRX is provided to allow everyone
to test these new modules

#### Install Vagrant and Vagrant plugin for Junos

Vagrant [installation instructions](https://www.vagrantup.com/docs/installation/)

Vagrant plugin installation
```
vagrant plugin add vagrant-junos
```

Once Vagrant is installed, you can start the topology
```
git clone https://github.com/JNPRAutomate/ansible-core-junos-examples.git
cd ansible-core-junos-examples
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

## junos_config
[Official documentation](https://docs.ansible.com/ansible/junos_config_module.html) on Ansible Website
### Add configuration lines on device
##### Change the hostname of the device
```
ansible-playbook pb.config.update_hostname.yaml
```
> this operation is idempotent, if executed twice, Ansible will not report change the second time.

##### Add description on multiple interfaces using a list as input
```
ansible-playbook pb.config.add_description.yaml
```
### Delete configuration lines on devices
```
ansible-playbook pb.config.delete_description.yaml
```

### Rollback configuration
```
ansible-playbook pb.config.rollback.yaml
```

## junos_command
[Official documentation](https://docs.ansible.com/ansible/junos_command_module.html) on Ansible Website

### Execute show system user and get response in JSON & XML
```
ansible-playbook pb.command.show_version.yaml
```

### Query interface status and validate response with wait_for
```
ansible-playbook pb.command.show_interface.yaml
```

## junos_facts
[Official documentation](https://docs.ansible.com/ansible/junos_facts_module.html) on Ansible Website

### Query facts and configuration in XML format on device
The configuration will be automatically converted from XML to JSON
```
ansible-playbook pb.facts.get_config_json_xml.yaml
```

### Query configuration in TEXT and save to a file
```
ansible-playbook pb.facts.get_config_txt.yaml
```

## junos_template
[Official documentation](https://docs.ansible.com/ansible/junos_template_module.html) on Ansible Website
### Generate a snippet of configuration based on a jinja2 template and deploy to device
```
ansible-playbook pb.template.push_interface.yaml
```

## junos_package
[Official documentation](https://docs.ansible.com/ansible/junos_package_module.html) on Ansible Website.  
Example not available yet

## junos_netconf
[Official documentation](https://docs.ansible.com/ansible/junos_netconf_module.html) on Ansible Website.  
Example not available yet
