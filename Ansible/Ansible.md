## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![lugrad90/Cybersecurity-Bootcamp/blob/main/Diagram/network_diagram.jpg](https://github.com/lugrad90/Cybersecurity-Bootcamp/blob/main/Diagram/network_diagram.jpg)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _/etc/ansible/my-elkservers.yml._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- A load balancer can add additional layers of security to your website without any changes to your application. The Web Application Firewall (WAF) in the load balancer protects your website from hackers.  
- Protects against unauthorized access, can detect and drop distributed denial-of-service (DDoS) traffic before it gets to your website.
- A load balancer simplifies compliance with PCI rules.
- What is the advantage of a jump box?:
- The advantage of a JumpBox is the orgination point for launching Administrative Tasks. This ultimately sets the JumpBox as a SAW (Secure Admin Workstation).
All Administrators when conducting any Administrative Task will be required to connect to the (SAW) JumpBox before perfoming any task/assignment.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches for log files/locations and collects log events.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB-1A   | Server   | 10.0.0.7   | Linux            |
| WEB-2A   | Server   | 10.0.0.8   | Linux            |
| JumpBox 2| Gateway  | 10.1.0.4   | Linux            |  
| ELK-1    | Server   | 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _Personal Home Public IP Address_(White listed)

Machines within the network can only be accessed by _____.
-Jump-Box-Provisioner VM/VNET IP 10.0.0.4
-JumpBox-2-ELK VM/VNET IP 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 104.45.221.5         |
| DVWA-VM1 | No                  | 10.0.0.7             |
| DVWA-VM2 | No                  | 10.0.0.8             |
| JumpBox 2| Yes                 | 23.100.84.107        |
| ELK-1    | No                  | 10.1.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You can input multiple commands into multiple servers with a single playbox.

The playbook implements the following tasks:
- Install: docker.10
- Install: python-pip
- Install: docker
- Command: sysctl -w vm.max_map_count=262144
- Launch Docker Container: elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![lugrad90/Cybersecurity-Bootcamp/blob/main/Ansible/Screenshot%202020-12-13%20153407.png](https://github.com/lugrad90/Cybersecurity-Bootcamp/blob/main/Ansible/Screenshot%202020-12-13%20153407.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- ELK-1 10.1.0.5

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat monitors log files and/or locations that are specified, collects all log events, and forwards them either to Elasticsearch or Logstash for indexing.
Filebeat collects all the changes that have been made.
![lugrad90/Cybersecurity-Bootcamp/blob/main/Ansible/kibana-system.png](https://github.com/lugrad90/Cybersecurity-Bootcamp/blob/main/Ansible/kibana-system.png) 
image taken from {https://www.google.com/search?q=filebeat+dashboard+example
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.
Metricbeat collects all metrics and statistics from the data.
![lugrad90/Cybersecurity-Bootcamp/blob/main/Ansible/metric2.png](https://github.com/lugrad90/Cybersecurity-Bootcamp/blob/main/Ansible/metric2.png)
image taken from {https://www.google.com/search?q=metricbeat+dashboard+example

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ root@9263bdb4a531:/etc/ansible/roles# filebeat-playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? {/etc/ansible/hosts} How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ {nano into the hosts file and add the IP addresses of the specific machine under the group headings webservers/elkservers. 
- _Which URL do you navigate to in order to check that the ELK server is running?  ELK-VM-Extrnal-IP-Addess:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
{root@container:/etc/ansible# ansible-playbook filebeat-playbook.yml

