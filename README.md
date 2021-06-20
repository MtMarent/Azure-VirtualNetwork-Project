## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/MtMarent/Azure-VirtualNetwork-Project/Diagrams/'virtual network map.png'

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the MtMarent-Azure-VirtualNetwork-Project-LocalRepository-Ansible file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/MtMarent/Azure-VirtualNetwork-Project/Ansible/MtMarent-Azure-VirtualNetwork-Project-LocalRepository-Ansible.txt

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected, in addition to restricting traffic to the network.
Load balancers allow you to add and subtract servers from the load balancing pool as demand dictates. The jump box costructed adds
another layer of security to your network, making sure that there is a buffer between the client and the virtual network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system servers.
- Filebeat keeps the state of each file and frequently flushes the state to disk in the registry file. The state is used to remember the last offset a harvester was reading from and to ensure all log lines are sent.
- Metricbeat records and periodically collects metrics from the operating system and from services running on the server and takes the metrics and statistics that it collects and ships them to the output that users specify.

The configuration details of each machine may be found below.

| Name     | Function | IP Address   | Operating System |
|----------|----------|--------------|------------------|
|          |          |              |                  |
| Jump Box | Gateway  | 10.0.0.4     | Linux            |
| Web-1    | Database | 10.0.0.6     | Linux            |
| Web-2    | Database | 10.0.0.7     | Linux            |
| Web-3    | Database | 10.0.0.8     | Linux            |
| Elk-1    | Monitor  | 10.1.0.5     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 5061 Kibana port

Machines within the network can only be accessed by the Jump Box.
- 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|          |                     |                      |
| Jump Box | Yes                 | 73.71.189.8          |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |
| Elk-1    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You can use the elk.yml file to easily increase the scale of networks and it can be deployed across multiple systems by executing the file.

The playbook implements the following tasks:
- Install Docker on system
- Install pip3 on system
- Increase the virtual memory of the system
- Download and Launch Elk Container Image

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/MtMarent/Azure-VirtualNetwork-Project/Images/'elk docker ps.png'

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6
- 10.0.0.7
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat allows us to collect data about the file system such as log events, and ships them out to be monitored.
- Metricbeat allows us to collect metrics and stats and ships them to the output specified.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to ansible.
- Update the update the host file to include the webserver and Elk
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Specific commands the user will need to run to download the playbook

- nano ansible.cfg
- add the machine, its IP, and ansible_python_interpreter=/usr/bin/python3 to the hosts
- Ctrl + x to exit file
- in the folder that install-elk.yml is in, run: cp install-elk.yml /etc/ansible
- nano install-elk.yml /etc/ansible
- name: installing elk hosts: [your_machine]
- Ctrl + x to exit file
- ansible-playbook install-elk.yml
