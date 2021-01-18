# Syntropy based monitoring stack

These ansible-playbooks and related files are for semi-automated monitoring stack (Grafana, Prometheus, Node-Exporter) deployment utilizing simplicity of network configuration provided by Syntropy agent and command line utilities.

# What is Syntropy?

Syntropy stack is software which lets you to easily establish VPN connections between remote endpoints, implement network-as-a-code approach and to avoid complex and inneficient newtork firewall and routing setups.


# Requirements

Debian/Ubuntu based distro and dependencies installed

# Dependencies

These are required for Syntropy network management via CLI:

```
apt install python3
apt install python3-pip
pip install git+https://github.com/SyntropyNet/syntropy-cli#egg=syntropycli
pip install git+https://github.com/SyntropyNet/syntropy-nac#egg=syntropynac
```

# How to run

Simply clone the code repository to your ansible server:
```
git clone https://github.com/jpacekajus/syntropy-grafana-prometheus-node-exporter.git
```
Update your inventory file accordingly:
```
cat /etc/ansible/hosts

[exporter_nodes]
exporter1
exporter2
exporterN

[prometheus_nodes]
prometheus1

[web_nodes]
grafana1

```
Update the variables in main.yml at the top directory:
```...
- name: Deploy Grafana
  become: true
  hosts: web_nodes
  vars:
    subnet: 172.1.0.0/24
    prometheus_ip: 172.2.0.2
    cloud_provider: '3
    api_key: MyAPIKey
    domain: 'grafana.mydomain.com'
    email: 'my@email.com'
...
```
Run the playbook:
```
ansible-playbook main.yaml
```
