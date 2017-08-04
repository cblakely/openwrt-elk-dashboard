# Ansible playbooks to build an ELK dashboard for OpenWRT

This was inspired by the work of others doing similar things for pfSense - see [here](https://forum.pfsense.org/index.php?topic=120937.0)

This repository contains two playbooks:
- elk.yml - This configures an Ubuntu 16.04 server VM into an ELK (elasticsearch/logstash/kibana) stack with the necessary filters and patterns to parse syslog messages generated by OpenWRT.
- dashboard.yml - This imports an example dashboard to visualize the data parsed.

### Setting up the VM
- Build an Ubuntu 16.04 Server VM and get it on the network
- Copy your SSH keys to the VM
- Edit the group_vars/elk.yml and inventory.ini files for your environment
- run the playbook with: `ansible-playbook -i inventory.ini elk.yml`

### Setting up OpenWRT
- I have tested this with chaos calmer and designate driver (aka built from master branch as there has not been a formal release of D/D yet).
- Everything you need is in System -> System -> Logging.
- External server should be the ELK VM IP address
- port should be `2514` (or use whatever you want and edit logstash to match)
- protocol: `UDP`
- log output level: `Info`

### Setting up the Dashboard
- run the playbook: `ansible-playbook -i inventory.ini dashboard.yml`

### Screenshot of the Dashboard

![Kibana Firewall Dashboard](http://i.imgur.com/O29FrXE.png)


