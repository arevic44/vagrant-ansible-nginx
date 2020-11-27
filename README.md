# Vagrant-Ansible-Nginx

A sample project to demonstrate the upstream module of Nginx. Default balancing method is used, requests are distributed between the servers using a weighted round-robin algorithm.

## Installation

1. Ensure that both [Vagrant](https://www.vagrantup.com/docs/installation) and [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) are installed on the host.
2. Configure setup in `hosts.yml`
3. Run Vagrant to setup virtual machines.

```
vagrant up
```

## Usage
To test network load balancing, connect a browser to the loadbalancer IP address, for example: http://192.168.17.10. Refresh the screen multiple times. If the cluster is operating successfully, web pages with hostnames of different machines in the cluster appear after each refresh.
