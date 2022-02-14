## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Alt text](https://github.com/CyberTarek/Security/blob/main/Diagrams/Network-Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/filebeat-playbook

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting high amounts of traffic to the network.
- Load balancer will defend the network against denial of service attacks (DOS). The Jumpbox provides a checkpoint that must be connected to before launching any more tasks. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs, files and system metrics.
- Filebeat will monitor and centralize log data, and then forward them to either Elasticsearch or Logstash
- Metricbeat will help monitor servers by collecting metrics from the system and services running on the server. Will take the metrics and statistics collected and output them to Elasticsearch or Logstash, or any output you specify.

The configuration details of each machine may be found below.

| Name                | Function | IP Address  | Operating System |
|---------------------|----------|-------------|------------------|
| JumpBox Provisioner | Gateway  | 40.78.8.100 | Linux            |
| Web-1               | Server   | 10.0.0.12   | Linux            |
| Web-2               | Server   | 10.0.0.13   | Linux            |
| Elk VM              | Server   | 10.1.0.4    | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 50.43.58.246

Machines within the network can only be accessed by the JumpBox Provisioner (40.78.8.100)
- My ELK VM is accessable only from my host computer (50.43.58.246).

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses            |
|---------------------|---------------------|---------------------------------|
| JumpBox Provisioner | Yes                 | Host Computer IP                |
| Web-1               | No                  | 10.0.0.10                       |
| Web-2               | No                  | 10.0.0.10                       |
| Elk VM              | No                  | Host (50.43.58.246) & 10.0.0.10 |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because you can now deploy the scripts onto multiple machines, and be sure that they run identically, and perform the exact same actions each time they are run.

The playbook implements the following tasks:
- Installs Docker
- Installs Python-pip
- Install Docker Python Module
- Download and Launch a Docker Web Container
- Enable Docker Services

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

~/Pictures/dockerps

### Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.12) & Web-2 (10.0.0.13)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat forwards and centralizes log data. It monitors the log files or locations that you specify, collects log events, and forwards them to Elasticsearch or Logstash for indexing
- Metricbeat collects metric data from the servers, such as CPU usage, memory or data related to services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible
- Update the host file to include webservers and elk server, as well as their IP addresses
- Run the playbook, and navigate to http://20.119.66.170:5601/app/kibana to check that the installation worked as expected.

# FAQ

# Which file is the playbook? Where do you copy it?
- /etc/ansible/configure-ELK.yml
- Copy it into the directory you keep your files in
# Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- Update the hosts file, make sure you include the ELK servers IP address
- Add the private IP's of the desired machines under "#servers"

# Which URL do you navigate to in order to check that the ELK server is running?
- http://20.119.66.170:5601/app/kibana
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

- ansible-playbook configure-ELK.yml  (Run playbook)
- nano hosts                          ( Edit hosts file)
- nano configure-ELK.yml              (Edit playbook) 
