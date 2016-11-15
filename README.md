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
* nova.yml is a part of nova role which i provided as a fix to instance boot issue using crudini

Target host(s) requirements

    * OS version: Ubuntu 14.04
    
    * The required Openstack repositories have to be properly configured.
    # apt-get install software-properties-common
    # add-apt-repository cloud-archive:mitaka
    # apt-get update && apt-get dist-upgrade
    # apt-get install python-openstackclient -y
    
    * SSH key passwordless authentication must be configured for root account.
     Ensure you have PermitRootLogin yes  in the /etc/ssh/sshd_config file
     Then change the password for root user using the command: passwd

    * se_linux must be disabled.
    setenforce 0
    
    * requiretty should be switched off in /etc/sudoers file.
    Run the command visudo and modify line as below:
    Defaults    !requiretty
    
    * 2 interfaces must be present: one for private and one for provider(public) network.
    at least one spare partition must be available for cinder( block storage ) service. The file resembles as below:
    
    root@controller:~# cat /etc/network/interfaces
    # interfaces(5) file used by ifup(8) and ifdown(8)
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 172.27.3.141
    gateway 172.27.3.1
    netmask 255.255.255.0
    dns-nameservers 8.8.8.8
    up ip link set dev $IFACE up
    down ip link set dev $IFACE down
    
    auto eth1
    iface eth1 inet static
    address 10.0.3.10
    netmask 255.255.255.0
    up ip link set dev $IFACE up
    down ip link set dev $IFACE down
     
    * Disable firewall using iptables -F
    
    * Remove 127.0.1.1 entry and replace 127.0.1.1 with the local_ip(eth0). The file must resemble as below:
    root@controller:~# cat /etc/hosts
    127.0.0.1       localhost
    #127.0.1.1      controller
    172.27.3.141    controller
    # This is my target vm to deploy openstack 
    
    * Copy public key from your Ansible installed host (master node) to target vm as:
    ssh-copy-id -i /path/to/id_rsa.pub root@172.27.3.141
   
The deployment starts with command execution " ansible-playbook -i hosts site.yml -v" as shown below:

  ![alt tag](https://github.com/npraveen35/Ansible_OpenStack_Works/blob/master/deployments_starts.JPG)

With approximate time of 20 to 40 minutes deployments halts as below.
   
  ![alt tag](https://github.com/npraveen35/Ansible_OpenStack_Works/blob/master/deployment_ends.JPG)

FYI given below are the references:

[1]http://docs.ansible.com/ansible/command_module.html

[2]https://github.com/muraliselva10/deploy-openstack-ansible/tree/mitaka-ubuntu
