## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible/playbook.yml file may be used to install only certain pieces of it, such as Filebeat.



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
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system monitoring.


The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Ansible          |
| Web 1    |Load Balance| 10.0.0.5 |Docker            |
| Web 2    |Load Balance| 10.0.0.6 |Docker            |
| Elk      |Analytics | 10.1.0.4   |Docker            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Bxx machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 75.32.201.129
- Public IP: 52.188.147.124
- Private IP: 10.0.0.4
  

Machines within the network can only be accessed by containers.
- dreamy blackwell container

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 75.32.201.129        |
| Web 1/2  | No                  | 10.0.0.4 or 52.188.147.124 |
| Elk      | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because almost anyone can do it


The playbook implements the following tasks:
- Install Docker
- Download Image
- edit yml to config correct IP addresses
- run with docker
- check for data on kibana page

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 52.188.147.124
  10.0.0.5
  10.0.0.6


We have installed the following Beats on these machines:
- filebeat
- metricbeat

Filebeat is a shipper that monitors log files and event and will forward them to Logstach or Elasticsearch. While metricbeat is also a shipper but collects metrics from the operating systems and services on the server, which will then be sent to the specified output whether it be Logstash or Elasticsearch

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat download file to /etc/ansible/files (once you change the config file you will move it to this same folder).
- Update the /etc/filebeat/filebeat-configuration.yml file to include your elk ip address (10.1.0.4) under the host configurations
- Run the playbook, and navigate to http://104.42.182.199:5601/app/kibana to check that the installation worked as expected.
