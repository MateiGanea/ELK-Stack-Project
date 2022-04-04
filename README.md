## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img src="https://raw.githubusercontent.com/MateiGanea/ELK-Stack-Project-WIP/main/images/network%20diagram.png" alt="network diagram">

These files have been tested and used to generate a live ELK deployment on Azure using Ansible. They can be used to either recreate the entire deployment pictured above. Alternatively, select playbook files may be used to install only certain pieces of it, such as Filebeat.

  <a href="https://github.com/MateiGanea/ELK-Stack-Project-WIP/blob/main/ansible/install_elk.yml">ELK playbook</a>
  /
  <a href="https://github.com/MateiGanea/ELK-Stack-Project-WIP/blob/main/ansible/pentest.yml">DVWA playbook</a>
  /
  <a href="https://github.com/MateiGanea/ELK-Stack-Project-WIP/blob/main/ansible/filebeat-playbook.yml">filebeat playbook</a>
  /
  <a href="https://github.com/MateiGanea/ELK-Stack-Project-WIP/blob/main/ansible/metricbeat_playbook.yml">metricbeat playbook</a>
  /

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be redundant, in addition to restricting malicious access to the network.
- This is a solution for availability

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- filebeat watches for system logs
- metricbeat monitors system performance/load status

The configuration details of each machine may be found below.

| Name     | Function | IP Address       | Operating System        |
|----------|----------|------------------|-------------------------|
| Jump Box | Gateway  | 20.53.232.160    | Ubuntu Server LTS 18.04 |
| Web-1    |          | 10.0.0.5         | Ubuntu Server LTS 18.04 |
| Web-2    |          | 10.0.0.6         | Ubuntu Server LTS 18.04 |
| ELK-1    |          | 20.219.111.249   | Ubuntu Server LTS 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet the webservers do not have public ip addresses. 

Machines within the network can only be accessed by my personal computer. However the load balancer could be exposed to the public internet to provide acces to the webservers providing redundancy as well as protecion from denial of service, I have chosen not to since this is a personal project and the webapps are vulnerable.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | my personal ip       |
| ELK-1    | No                  | my ip, 10.0.0.4      |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- the results are easily reproducable since the configs are reusable
- elimination of human error in instalation 

The playbook implements the following tasks:
- Install Docker
- Install Python3-PIP
- Allocate virtual memory
- Download install and config ELK
- Set to automatically start on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="https://raw.githubusercontent.com/MateiGanea/ELK-Stack-Project-WIP/main/images/docker%20ps.png" alt="docker ps">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Metricbeat
- Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to look at live log data from both webservers this means we can monitor events such as failed ssh logins and sudoing
- metricbeat enables monitoring of all kinds of system data such as cpu usage, memory usage and network activity

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible inside the ansible container on the jumbox.
- Update the hosts file to include the intended elk and webservers private ip addresses
- Run the playbook, and navigate to http://20.219.111.249:5601/ (example) to check that the installation worked as expected.

`wget https://raw.githubusercontent.com/MateiGanea/ELK-Stack-Project-WIP/main/ansible/install_elk.yml`

make sure to edit all config files

`ansible-playbook elk.yml`
