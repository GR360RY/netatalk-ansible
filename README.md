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
    
Testing Setup with Vagrant
-------------------

Vagrantfile includes the number of Linux Distros. To test specific distribution check the contents of Vagrantfile
and choose on of the distros:

    config.vm.define :ubuntu1204 do |ubuntu1204|
      # Ubuntu Server 12.04 amd64 Minimal from files.vagrantup.com
      ubuntu1204.vm.box = "precise64"
      ubuntu1204.vm.box_url = "http://files.vagrantup.com/precise64.box"
      ubuntu1204.vm.network "public_network"
      ubuntu1204.vm.provider :virtualbox do |vbox|
        vbox.customize ['modifyvm', :id, '--memory', '1024']
      end
    end
    config.vm.define :ubuntu1210 do |ubuntu1210|
      # Ubuntu Server 12.10 amd64 Minimal (VirtualBox 4.2.6) from http://www.vagrantbox.es/
      ubuntu1210.vm.box = "quantal64"
      ubuntu1210.vm.box_url = "http://goo.gl/wxdwM"
      ubuntu1210.vm.network "public_network"
      ubuntu1210.vm.provider :virtualbox do |vbox|
        vbox.customize ['modifyvm', :id, '--memory', '1024']
      end
    end
          
To test specific distribution, say Ubuntu 12.04, run the next command:

    vagrant up ubuntu1204
    
If there is an issue with bringing up one of the VMs and you receive the next error:

    fatal: [os_name] => SSH encountered an unknown error during the connection. We recommend you re-run the command using -vvvv, which will enable SSH debugging output to help diagnose the issue

Update your ~/.ssh/config file by adding the next block for localhost:

    Host 127.0.0.1 localhost
      StrictHostKeyChecking no
      UserKnownHostsFile /dev/null
