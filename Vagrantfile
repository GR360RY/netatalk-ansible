VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  machines = {
    'ubuntu1204'=> {
      'define' => :ubuntu1204,
      'box' => "ubuntu/precise64",
      'name' => "ubuntu1204"
    },
    'ubuntu1210'=> {
      'define' => :ubuntu1210,
      'box' => "chef/ubuntu-12.10",
      'name' => "ubuntu1210"
    },
    'ubuntu1304'=> {
      'define' => :ubuntu1304,
      'box' => "chef/ubuntu-13.04",
      'name' => "ubuntu1304"
    },
    'ubuntu1310'=> {
      'define' => :ubuntu1310,
      'box' => "chef/ubuntu-13.10",
      'name' => "ubuntu1310"
    },
    'ubuntu1404'=> {
      'define' => :ubuntu1404,
      'box' => "ubuntu/trusty64",
      'name' => "ubuntu1404"
    },
    'ubuntu1410'=> {
      'define' => :ubuntu1410,
      'box' => "chef/ubuntu-14.10",
      'name' => "ubuntu1410"
    }
  }

  machines.each do |os,param|
    config.vm.define param['define'] do |vbox|
      vbox.vm.provision "ansible" do |ansible|
        ansible.playbook = "netatalk.yml"
        ansible.groups = {"netatalk" => [param['name']]}
      end
      vbox.vm.box = param['box']
      vbox.vm.hostname = param['name']
      vbox.vm.network "public_network"
      vbox.vm.provider :virtualbox do |box|
        # box.customize ['modifyvm', :id, '--memory', '1024']
        box.customize ["modifyvm", :id, "--name", param['name'] ]
      end
    end
  end

end
