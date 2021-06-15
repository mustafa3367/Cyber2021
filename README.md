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


Availability Zone 1: DVWA 1 + DVWA 2


Availability Zone 2: ELK


ELK Server Configuration

The ELK VM exposes an Elastic Stack instance. Docker is used to download and manage an ELK container.

Rather than configure ELK manually, we opted to develop a reusable Ansible Playbook to accomplish the task. This playbook is duplicated below.

To use this playbook, one must log into the Jump Box, then issue: ansible-playbook install_elk.yml elk. This runs the install_elk.yml playbook on the elk host.
Access Policies

The machines on the internal network are not exposed to the public Internet.
Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the IP address 64.72.118.76




Machines within the network can only be accessed by each other. The DVWA 1 and DVWA 2 VMs send traffic to the ELK server.
A summary of the access policies in place can be found in the table below.

Name	 Publicly  Accessible	Allowed IP Addresses

Jump Box	Yes     	       64.72.118.76

ELK     	No	             10.0.0.1-254

DVWA 1  	No	             10.0.0.1-254

DVWA 2  	No	             10.0.0.1-254


Elk Configuration

The ELK Stack is a collection of three open-source products — Elasticsearch, Logstash, and Kibana. ELK stack provides centralized logging in order to identify problems with 

servers or applications. It allows you to search all the logs in a single place. It also helps to find issues in multiple servers by connecting logs during a specific time frame.

we used the ELK to preform a connection between all the three VM Boxes. Ansible was used to automate configuration of the ELK machine.

The below is playbook been used.



<img width="433" alt="2" src="https://user-images.githubusercontent.com/78521992/121988381-cbd12280-cd5f-11eb-92a2-7da267647905.png">



<img width="406" alt="Screenshot 2021-06-14 222648" src="https://user-images.githubusercontent.com/78521992/121988382-cc69b900-cd5f-11eb-856b-6ccdf37bcde5.png">

Target Machines & Beats


This ELK server is configured to monitor the DVWA 1 and DVWA 2 VMs, at 10.0.0.5 and 10.0.0.6, respectively.

We have installed the following Beats on these machines:


Filebeat

Metricbeat

Packetbeat

These Beats allow us to collect the following information from each machine:

Filebeat: Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs.

Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.

Packetbeat: Packetbeat collects packets that pass through the NIC, similar to Wireshark. We use it to generate a trace of all activity that takes place on the network, in case later forensic analysis should be warranted.

The playbook below installs Metricbeat on the target hosts. The playbook for installing Filebeat is not included, but looks essentially identical — simply replace metricbeat with filebeat, and it will work as expected.


<img width="674" alt="1" src="https://user-images.githubusercontent.com/78521992/121989022-04253080-cd61-11eb-9d21-cc64c2ddd054.png">


<img width="425" alt="3" src="https://user-images.githubusercontent.com/78521992/121989025-04253080-cd61-11eb-987a-b0427f7a32fa.png">


Using the Playbooks
In order to use the playbooks, you will need to have an Ansible control node already configured. We use the jump box for this purpose.

To use the playbooks, we must perform the following steps:

-Copy the playbooks to the Ansible Control Node

-Run each playbook on the appropriate targets



The easiest way to copy the playbooks is to use Git:


<img width="405" alt="5" src="https://user-images.githubusercontent.com/78521992/121989253-68e08b00-cd61-11eb-8df1-40cb6d93719d.png">


This copies the playbook files to the correct place.


Next, you must create a hosts file to specify which VMs to run each playbook on. Run the commands below:

<img width="634" alt="6" src="https://user-images.githubusercontent.com/78521992/121989378-a6451880-cd61-11eb-806a-79cb4cf44423.png">

After this, the commands below run the playbook:

<img width="572" alt="7" src="https://user-images.githubusercontent.com/78521992/121989463-cd9be580-cd61-11eb-85b3-b3f8f8b5769c.png">

To verify success, wait five minutes to give ELK time to start up.

Then, run: curl http://10.0.0.8:5601. This is the address of Kibana. If the installation succeeded, this command should print HTML to the console.







