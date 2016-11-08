# Ansible_OpenStack_Works

The scripts here are part of my code contribution[2] worked along with my fellow colleagues.

Ansible scripts are used to deploy basic services of OpenStack Mitaka on Ubuntu 14.04.

 * keystone
 * nova
 * neutron (linuxbridge as mechanism driver)
 * glance
 * cinder
 * horizon

* neutron folder is the ansible role for deploying neutron service.
* nova.yml is a part of nova role which i provided as a fix to instance boot issue.

The deployment starts with command execution " ansible-playbook -i hosts site.yml -v" as shown below:

  ![alt tag](https://github.com/npraveen35/Ansible_OpenStack_Works/blob/master/deployments_starts.JPG)

With approximate time of 20 to 40 minutes deployments halts as below.
   
  ![alt tag](https://github.com/npraveen35/Ansible_OpenStack_Works/blob/master/deployment_ends.JPG)

FYI given below are the references:

[1]http://docs.ansible.com/ansible/command_module.html

[2]https://github.com/muraliselva10/deploy-openstack-ansible/tree/mitaka-ubuntu
