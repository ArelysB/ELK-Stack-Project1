# ELK-Stack-Project1
Azure cloud network design and ELK server configuration.
## This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build

### Drescription of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting DDoS attacks to the network.
The files listed in this repository were used to configure the network presented below
![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Network-Diagram/ELK-Stack-Project1-Network_Diagram.PNG)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project1-Network_Diagram file may be used to install only certain pieces of it, such as Filebeat.

#### Jump box
- Region: East US
- Private IP: 10.0.0.4
- Public IP (static): 13.82.3.71

#### NewDVWA-VM1
- Region: East US2
- Availability zone: 1
- Private IP: 10.1.0.4
- Public IP: none

#### NewDVWA-VM2
- Region: East US2
- Availability zone: 1
- Private IP: 10.1.0.5
- Public IP: none

#### ELK-VM
- Region: East US2
- Availability zone: 2
- Private IP: 10.1.0.9
- Public IP: 20.186.27.100

#### Firewall (Network Security Group JumpBox nsg)
- Add whitelist of IPs: for the IP addresses that are allowed to the network.
- Setup inbound rules to only allow the IP in the whitelist access to the jump-box from the external network and monitoring.

#### Peering
- The peering was added in order to make possible the two regions  to communicate with each other.

#### Load balancer
- Fronted IP Configuration:40.70.156.45 (Front_End-LB-RedTeam)
- Backend pools: NewDVWA-VM1 and qDVWA-VM2
- Health probes: setup for load balancing rule and detect the failure of an application on a backend endpoint.
- Load balancing rules: open port 80 for HTTP

#### What aspect of security do load balancers protect? 

Load balancers are used to reroute traffic in real-time from one server to another in the event of a DDoS attack, to prevent the server becoming unavailable. And because of this, load balancers help to eliminate single points of failure, reduce the attack surface, and make it harder to exhaust resources and saturate links.

#### What is the advantage of a jump box?
A jump box is a secure computer that is used for system admins as an SSH gateway to a remote network. Jump boxes act as a bridge between different security zones and offer secure and controlled access to such networks. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

#### What does Filebeat watch for?

Filebeat monitors the log files or locations that specified by system admins collects log events and forwards them either to Elasticsearch or Logstash for indexing

#### What does Metricbeat record?

Metricbeat helps monitor servers and the services they host by collecting metrics (such as uptime and CPU usage) from the operating system and services. 


The configuration details of each machine is found below.

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/IP-config.PNG)



## Playbook files:
- [Webservers](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/webserversYML.txt)
- [Filebeat-playbook.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/filebeatsyml.txt)
- [Elk_Playbook.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/ELK_Playbook.txt)
- [Metricbeat.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/MetricbeatsYML.txt)


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the *Jump-Box* machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address 73.106.28.69 (my local workstation).

#### Add whitelisted IP addresses

Machines within the network can only be accessed by Jump-Box.
Which machine did you allow to access your ELK VM? *Jump-Box-Provisioner* What was its IP address? *The Jump-Box 10.1.0.9*

A summary of the access policies in place can be found in the table below.

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/VMsAccessibility.PNG)

### Elk Configuration
Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually. 

One of the advantages of Ansible is that it allows to quickly and easily deploy multi layer apps. So it is not necessary to write custom code to automate systems; once the tasks  list required to be done by writing a playbook are defined,  Ansible will figure out how to get the systems to deploy the playbooks in the way  system admins want them to be.

#### The Process 
##### 1- SSH into the jump Box:

`ssh Red-sysadmin@13.82.3.71`

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/SSH%20into%20Jump-Box.PNG)

##### 2- Start and attached to the ansible docker: 

`sudo docker start elegant_sutherland`

`elegant_sutherland`

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Starting%20and%20attaching%20the%20Ansible%20container.PNG)

##### 3- Go to /etc/ansible/ and created the [ELK playbook](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/ELK_Playbook.txt)

using the command `nano Elk_Playbook.yml`

##### 4- Run Elk_Playbook.yml

`nano ansible-playbook Elk_Playbook.yml`

##### 5- SSH into the ELK-VM to verify ELK is up and running
`ssh ansible@10.1.0.9`

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/SSH%20into%20ELK-VM.PNG)


Run the commands `sudo docker start elk` to start the container and `sudo docker ps` verify that the container is running.

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Starting%20the%20ELK%20service.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

#### NewDVWA-VM1: 10.1.0.4
#### NewDVWA-VM2: 10.1.0.5

We have installed the following Beats on these machines:

These Beats allow us to collect the following information from each machine:


- Filebeat:  monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. The Filebeat Elasticsearch module can handle audit logs, deprecation logs, gc logs, server logs, and slow logs.

- Metricbeat collects a variety of metrics from your server (i.e., operating system and services) and ships them to an output destination of your choice. These destinations can be ELK components such as Elasticsearch or Logstash or other data processing platforms such as Redis or Kafka.


### Using the Playbooks

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Create the [filebeat-configuration.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Linux/filebeat-configuration.txt)  file to /etc/ansible/roles/files
- Update the filebeat-configuration.yml file to include the ELK-VM private IP in lines 1106 and 1806. Use de command `nano filebat-configuration.yml`
- Run the playbook, and navigate to http://20.186.27.100:5601 (ELK-VM public IP and Kibana port) to check that the installation worked as expected (access to the Kibana GUI). I went to Filebeat ⇒ Add Data ⇒ System logs to check Module status 

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Filebeatstatus.PNG)

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Filebeat%20Syslog.PNG)

With Filebeat it is possible to monitor not only system logs, but attempts to SSH connections and sudo commands too.

- SSHconnections

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Filebeat%20SSH%20login%20attempts.PNG)

- Sudo commands
![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Filebeat%20Sudo%20commands.PNG)

Explore the options to build useful statistics.

### Filebeat instalation.

#### Playbookfile:
[Filebeat-playbook.yml]https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/filebeatsyml.txt()

- Create the [filebeat-configuration.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Linux/filebeat-configuration.txt)  file to /etc/ansible/roles/files
- Update the filebeat-configuration.yml file to include the ELK-VM private IP in lines 1106 and 1806. Use de command `nano filebat-configuration.yml`

#### Where do you copy it?
 /etc/ansible/roles/

#### Which file do you update to make Ansible run the playbook on a specific machine? 
The [hots](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Linux/hosts.txt) file, located in /etc/ansible/hosts
   For this task use the command `nano hosts`

#### How do I specify which machine to install the ELK server on versus which to install Filebeat on?
For the ELK, creat a new group called [elkservers] and under it, type in the ELK-VM private IP. For the filebeat install, I just left the NewDVWA-VM 1 and NewDVWA-VM 2 IP addresses under the group [webservers]. 

#### Which URL do you navigate to in order to check that the ELK server is running?

http://20.186.27.100:5601 

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/KibanaGUI-Access.PNG)


### Metricbeat instalation.

#### Playbookfile:

[Metricbeat.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/MetricbeatsYML.txt)

- Create the [metricbeat-configuration.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Linux/metricbeatyml.txt)  file to /etc/ansible/roles/files
- Update the metricbeat-configuration.yml file to include the ELK-VM private IP in lines 62 and 96. Use de command `nano metricbeat-configuration.yml`

#### How do I specify which machine to install the ELK server on versus which to install Filebeat on?
For the ELK, creat a new group called [elkservers] and under it, type in the ELK-VM private IP. For the filebeat install, I just left the NewDVWA-VM 1 and NewDVWA-VM 2 IP addresses under the group [webservers]. 

#### Which URL do you navigate to in order to check that the metricbeate service is running?

http://20.186.27.100:5601 

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/KibanaGUI-Access.PNG)

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Metricbeat%20Module%20status.PNG)

![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Images/Metricbeat%20Docker%20overview1.PNG)

