
Eric Nicholson
Eric.Nicholson@augustschell.com

These ansible playbooks were writen to be called from a Jenkins project for automation of common Splunk tasks. There were three
tools involved for the automation. GitHub, Jenkins and Ansible.


Ansible Hosts File
------------------

ansible_hosts_example.txt is a sample of the hosts file I used. 
The location of the anisible host file is:  /etc/ansible/hosts

Here is the layout of the file the way I used it:

The stanza contains the hostname to be used within the playbook.
[cirt_deployer]
cirt_sh_deployer ansible_hosts=123.69.1.100 ansible_user=ec2-user ansble_ssh_private_key_file=/data/pemkeys/PRDDPLKEY.pem
^^^^^^^^^^^^^^^^ 
This can be the FQDN. However, in my use case I relied on the "ansible_hosts" variable and used this field
a recognizable hostname which I could use in variables within the playbook. For example, in the splunkn_backup.yml I have a 
variable for the filename where this was used. It was also displayed in the Jenkins log files.

ansible_hosts = IP address of server
ansible_user  = User name to login with
ansible_ssh_private_key_file = For the use above


Playbook Descriptions
---------------------

Search Head Cluster Deployer
 - cirt_search_center.yml     = Eneterprise Security Search Center
 - cis_search_center.yml      = Cyber Information Systems
 - platform_search_center.yml = AWS App, DFARS etc...

Searh Head - Stand alone
 - lmx_search_center.yml = Microsoft Exchange = Used soley for this purpose
 - oic_search_center.yml = ITSI Search Head
 - plt_stg_deploy.yml    = Platform Staging search head
 - cis_stg_deploy.yml    = CIS Staging search head
 
Deployment Server
-----------------
deployment_server_prim.yml = There were two load balanced deployment servers. This playbook synced to both servers.

AWS Actions
-----------
manual_start.yml = Start an EC2 instance
manual_stop.yml  = Stop an EC2 instance

Splunk Backup
-------------
splunk_bakcup.yml = Backed up /opt/splunk/etc on the servers and synced to an AWS S3 Bucket

