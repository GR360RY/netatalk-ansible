Automated Installation of Netatalk 3.0.X
============

Full instructions are available here: [Blog Post](http://gr360ry.github.io/blog/2013/11/16/automating-installation-of-netatalk-3-dot-0-x-with-ansible/)

This ansible playbook will compile latest Netatalk 3.0.X from source and configure afp shares and Time Machine on your system.

System Requirements for Target System
----------

* Ubuntu 12.04 and 12.10
* Ansible installed on target system or on any other OS that has ssh access to targed system.

Step 2: Modify your user and shares list
-----------

* Clone ansible
* Edit netatalk.yml and change "user: vagrant" to your actual user with sudo privileges
* Edit vars/user_defined.yml and update share names and paths at the top of the yml file
* Modify ansible_hosts with the IP of your host ( actual IP or loopback 127.0.0.1 )

Step 3: Run ansible
------------

    cd netatalk-ansible
    ansible-playbook -i ./ansible_hosts netatalk.yml

Testing Setup with Vagrant
-------------------

Vagrantfile includes the number of Linux Distros. To test specific distribution check the contents of Vagrantfile
and choose one of the distros:

To test specific distribution, say Ubuntu 12.04, run the next command:

    vagrant up ubuntu1204

If there is an issue with bringing up one of the VMs and you receive the next error:

    fatal: [os_name] => SSH encountered an unknown error during the connection. We recommend you re-run the command using -vvvv, which will enable SSH debugging output to help diagnose the issue

Update your ~/.ssh/config file by adding the next block for localhost:

    Host 127.0.0.1 localhost
      StrictHostKeyChecking no
      UserKnownHostsFile /dev/null
