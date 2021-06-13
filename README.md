# ELK-PROJECT

Description of the Topology.
This repository includes code defining the infrastructure below.

<img width="584" alt="new HW 13" src="https://user-images.githubusercontent.com/78521992/121824990-94864700-cc75-11eb-9115-1584ca5d9013.png">

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the "D*mn Vulnerable Web Application"
Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network. The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users — namely, ourselves — will be able to connect in the first place.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network, as well as watch system metrics, such as CPU usage; attempted SSH logins; sudo escalation failures; etc.
The configuration details of each machine may be found below.

Name	Function	IP Address	Operating System
Jump Box	Gateway	10.0.0.4	Linux
DVWA 1	Web Server	10.0.0.5	Linux
DVWA 2	Web Server	10.0.0.6	Linux
ELK	Monitoring	10.0.0.8	Linux



In addition to the above, Azure has provisioned a load balancer in front of all machines except for the jump box. The load balancer's targets are organized into the following availability zones:
•	Availability Zone 1: DVWA 1 + DVWA 2
•	Availability Zone 2: ELK
ELK Server Configuration
The ELK VM exposes an Elastic Stack instance. Docker is used to download and manage an ELK container.
Rather than configure ELK manually, we opted to develop a reusable Ansible Playbook to accomplish the task. This playbook is duplicated below.
To use this playbook, one must log into the Jump Box, then issue: ansible-playbook install_elk.yml elk. This runs the install_elk.yml playbook on the elk host.
Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the IP address 64.72.118.76




Machines within the network can only be accessed by each other. The DVWA 1 and DVWA 2 VMs send traffic to the ELK server.
A summary of the access policies in place can be found in the table below.
Name	Publicly Accessible	Allowed IP Addresses
Jump Box	Yes	64.72.118.76
ELK	No	10.0.0.1-254
DVWA 1	No	10.0.0.1-254
DVWA 2	No	10.0.0.1-254
Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
