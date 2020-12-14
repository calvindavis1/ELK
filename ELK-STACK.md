## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/calvindavis1/ELK/blob/main/Diagrams/Network_Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/calvindavis1/ELK/blob/main/Ansible/Elk_YML.yml

https://github.com/calvindavis1/ELK/blob/main/Ansible/MetricBeat_YML.yml

https://github.com/calvindavis1/ELK/blob/main/Ansible/FileBeat_YML.yml

https://github.com/calvindavis1/ELK/blob/main/Ansible/Docker_YML.yml


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.


Load balancing ensures that the application will be highly accessible, in addition to restricting unwanted traffic to the network. The load balancer distributes traffic across the webservers, ensuring that a single webserver does not get overwhelmed. Using a jump box to configure these protects the server from unauthorized administrative access, while allowing administration easy access.

 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system files, traffic, and potential attacks.

- Filebeat watches for log data or changes in locations that you specify, creates log data and then ships it to Elasticsearch or Logstash to be sorted and possibly examined.

- Metricbeat records the metrics taken from the opererating system and from services running on the server in order to to create an analysis of the operations and tasks being run on the service.

The configuration details of each machine may be found below.

\begin{table}[]
\begin{tabular}{llll}
Name     & Function      & IP Address     & Operating System \\
Jump Box & Gateway       & 10.0.0.1       & Linux            \\
Web-1    & Server        & 10.0.0.7       & Linux            \\
Web-2    & Server        & 10.0.0.8       & Linux            \\
Web-3    & Server        & 10.0.0.9       & Linux            \\
ELK      & Server        & 10.1.0.4       & Linux            \\
LB       & Load Balancer & 52.191.136.128 & N/A             
\end{tabular}
\end{table}

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

76.25.65.45
192.168.0.7
*My host IP*


Machines within the network can only be accessed by Jumpbox and ELK server.

I allowed the JumpBox machine access to the ELK VM. It has an IP address of 76.25.65.45.

A summary of the access policies in place can be found in the table below.

\begin{table}[]
\begin{tabular}{lll}
Name          & Publicly Accessible & Allowed IP Addresses \\
JumpBox       & Yes                 & *My.Host.Machine.IP* \\
ELK           & Yes                 & 10.0.0.4/32          \\
Load Balancer & Yes                 & Any                  \\
Web Servers   & No                  & 52.146.45.9(LB)     
\end{tabular}
\end{table}

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automating configuration with Ansible provides an ease of the production of an unlimitted amount of servers to be configured as needed, without having to access each server individually.

The playbook implements the following tasks:

- Downloads and configures ELK/Kibona on the designated ELK server using Docker.
- Downloads and configures FileBeat and MetricBeat on the DVWA/Webservers.
- Donwloads and configures DVWA on the Webservers.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/calvindavis1/ELK/blob/main/Diagrams/Docker%20PS..png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.8
- 10.0.0.9

We have installed the following Beats on these machines:

- MetricBeat and Filebeat

These Beats allow us to collect the following information from each machine:

- FileBeat will allow us to see all of the logins/login attempts as well as changes to the system and any attempts to use elevated privelege.

- MetricBeat shows us how much traffic there is on the Web Servers by tracking the memory and cpu usage. If there is an unusual change in traffic, we will be able to see it by using MetricBeat.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk playbook file to the ansible container.
- Update the /ansible/host file to include all of the IP addresses of the servers that you would like to make your instalation on.

- Run the playbook, and navigate to http://elkserverip:5601/app/kibana to check that the installation worked as expected.


- The playbookfiles are Elk_YML.yml, Docker_YML.yml, and MetricBeat_YML.yml and they need to be copied to /etc/ansible/roles

- You will need to update the /etc/ansible/host file to include the IP addresses of the servers you would like to configure. Edit the /ect/ansible/host file and add the public IP's of the servers you would like to configure the ELK server on and the public IP's of the servers you would like to install FileBeat or MetricBeat on.

- _Which URL do you navigate to in order to check that the ELK server is running?

To check to see whether or not the ELK server is running, navigate to you internet browser and go to the following address:

http://"elkserverpublicip":5601/app/kibana