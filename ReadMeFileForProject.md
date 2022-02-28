## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](/images/FinalProject1Snip.PNG)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Filbeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - metricbeat-playbook.yml
  - install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting in-bound access to the network.
- Load balancers helps mitigate DDos attacks. The way it helps is by balancing the traffic so one server does not get overload its distributed evenly between the servers. In our project we had added a health probe which helps check our machines such as if a machine has an issue its reported and traffic is no longer sent there. The jumpbox advantage is that its limiting access to our virtual machines such as in our project in order to get access to them you need the private IPs. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Jump-Box and system network.
- The Filebeat watches for updates in files that are specified by the user in other words in collects log events
- Metricbeat records the system abd services running on the server

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function  | IP Address | Operating System |
|-----------|-----------|------------|------------------|
| Jump Box  | Gateway   | 10.0.0.1   | Linux Ubuntu     |
| Web-1     | Web Server| 10.0.0.8   | Linux Ubuntu     |
| Web-2     | Web Server| 10.0.0.9   | Linux Ubuntu     |
| ELK-Server| Monitoring| 10.1.0.4   | Linux Ubuntu     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 107.204.186.170

Machines within the network can only be accessed by jump box provisioner.
- Machine allowed to access the ELK VM: Jump-Box-Provisioner
- The IP address is: 40.78.154.170

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box | Yes                 | 107.204.186.170            |
| Web-1    | No                  | 10.1.0.4                   |
| Web-2    | No                  | 10.1.0.4                   |
| Elk      | Yes                 | 107.204.186.170 (Port 5601)|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because we don't have to configure ELK manually which is less human error and it automatically installs the packages that is needed. 

The playbook implements the following tasks:
- Installs docker.io package
- Installs python3-pip package
- Downloads the Docker elk container
- Enables the Docker service on boot
- The ELK requires more memory so the max count is set to 262144


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 IP address: 10.0.0.8
- Web-2 IP address: 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log information about your file system, an example would be updating a file and checking to see in Kibana if there were data collected. 
- Metricbeat collects metrics of our operating system and services running on the server. An example would be of what we expect to see is statistics based on a specific system.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/roles.
- Update the /etc/ansiblhosts file to include ip addresses of our VM machines under the two groups one for web servers and the other for elk
- Run the playbook, and navigate to Kibana (using URL 104.211.33.47:5601/app/kibana to check that the installation worked as expected.

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

**Important Note:** Before starting go to your Ansible container add the VM machines on the Ansible's host files. You will add your VMs ip addresses under the groups such as:
- webservers group: web-1 IP address and web-2 IP address
- elk group: elk VM IP address

Create your playbook command: touch [filepath name]/[playbook name].yml
Edit your playbook command: nano [playbook].yml
Add commands to install commands and specify which host (look at my filebeat-playbook.yml as an example or you can copy that information to your playbook)
Save playbook: CTRL + x
Enter yes 
Run playbook command: ansible-playbook [playbook name].yml

--**Repeat steps for metricbeat-playbook.yml**
