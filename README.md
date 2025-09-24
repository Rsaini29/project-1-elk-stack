
## Automated ELK Stack Deployment
<br>
The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/Rsaini29/Azure_Project/blob/main/Images/Network_Diagram.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of this project file may be used to install only certain pieces of it, such as Filebeat.

[Filebeat Playbook](https://github.com/Rsaini29/Azure_Project/blob/main/Images/filebeat_playbook%20yml_file.rtf)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- A load balancer performs an SSL offload- becoming an endpoint for SSL communication and managing encryption and decryption instead of performing it on the server. Load balancers also provide network segmentation and perform the TCP offloads as well, removing the overhead from servers, managing all of the TCP handshakes. 
- The advantage of a Jump Box is to be a gateway for all other devices- in our case VMs. Since users are only allowed to SSH into the Jump Box, other devices are isolated from potential threat actors. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configurations and system files.
- Filebeat watches for anomalies in our log files, parsing through data and allowing one to visualize and track the behavior of our services and applications. 
- Metricbeat records the statistics of our server usage and ships them to other third party services- to be further analyzed by security analysts. 



| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | Webserver| 10.0.0.5   | Linux            |
| Web-2    | Webserver| 10.0.0.6   | Linux            |
|ELK-SERVER| Monitor  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the host machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 98.XX.XXX.XXX

Machines within the network can only be accessed by internal users. 
- The machine that is allowed to access my ELK VM is my personal machine at 98.XX.XXX.XXX

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |      Yes            |    98.XX.XXX.XXX     |
| Web-1    |      No             |     10.0.0.5         |
| Web-2    |      No             |     10.0.0.6         |
|ELK-SERVER|      No             |     10.1.0.4         |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of using automatic configuration for ansible is that YAML files are able to perform smoother management and automation of tasks over other languages.

The playbook implements the following tasks:
- Ansible and Docker were installed on the Jump Box VM via an SSH sessions, allowing us to run our playbooks and automate the deployment of services/software
- A container on ansible was started and attached and an ELK VM was added to our NSG as a monitoring server
- Configuration files were created (ELK and ansible playbooks) and used to push out specific tasks on our Ansible playbooks for all required machines.



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.05 (Web-1) and 10.0.06 (Web-2) 

We have installed the following Beats on these machines:
- We installed Metricbeat and Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeat keeps track of the machine's metrics and gives statistics to analysts. An example of this would be the CPU utilization
and memory usage that is used during sessions. Filebeat on the other hand collects data from log files while keeping track of changes made to any sensitive files. For instance if a password or shadow file was altered, Filebeat would detect these anomalies and alert us of any suspicious activity. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible/roles.
- Update the hosts file to include your web server VMs and Elk server
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.


- The hosts file is in the playbook. It is copied to /etc/ansible/filebeat-playbook.yml
- The /etc/ansible/hosts file is updated to make Ansible run the playbook on a specific machine. We specify the machine to install the ELK server by specifying the machine's IP address. 
- The URL used to navigate in order to check the ELK server is running is: http://40.83.138.201:5601/app/kibana

