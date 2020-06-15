# ELK-Stack-Project1

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


Azure cloud network desgin and ELK server configuration.
The files listed in this repository were used to configure the network presented below
![](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Network-Diagram/ELK-Stack-Project1-Network_Diagram.PNG)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project1-Network_Diagram file may be used to install only certain pieces of it, such as Filebeat.
## Enter the playbook files:
- [Webservers](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/webserversYML.txt)
- [Filebeat-playbook.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/filebeatsyml.txt)
- [Elk_Playbook.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/ELK_Playbook.txt)
- [Metricbeat.yml](https://github.com/ArelysB/ELK-Stack-Project1/blob/master/Ansible/MetricbeatsYML.txt)





### Access Policies

