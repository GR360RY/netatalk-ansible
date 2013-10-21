Automated Installation of Netatalk 3.0.X
============

This istructions are for Ubuntu 12.04. The procedure for other Ubuntu version or Debian should be similar but not tested yet.

System Requirements
----------

* Ubuntu 12.04 Server or Desktop version
* Ansible installed on target system or on any other OS that has ssh access to targed system.

Step 1: Installing Ansible on target system
----------

On Ubuntu run the following commands:

    $ sudo add-apt-repository ppa:rquillo/ansible
    $ sudo apt-get update
    $ sudo apt-get install ansible
    
Step 2: Modify your user and shares list
-----------

* Clone ansible
* Edit netatalk.yml and change "user: vagrant" to your actual user with sudo privileges
* Edit netatalk.yml and update share names and paths at the top of the yml file
* Modify ansible_hosts with the IP of your host ( actual IP or loopback 127.0.0.1 )

Step 3: Run ansible
------------
    
    cd netatalk-ansible
    ansible-playbook -i ./ansible_hosts netatalk.yml
    
