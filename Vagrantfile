VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  machines = {
    'ubuntu1204'=> {
      'define' => :ubuntu1204,
      'box' => "precise64",
      'url' => "http://files.vagrantup.com/precise64.box",
      'name' => "ubuntu1204"
    },
    'ubuntu1210'=> {
      'define' => :ubuntu1210,
      'box' => "quantal64",
      'url' => "http://goo.gl/wxdwM",
      'name' => "ubuntu1210"
    },
    'ubuntu1304'=> {
      'define' => :ubuntu1304,
      'box' => "raring64",
      'url' => "http://goo.gl/ceHWg",
      'name' => "ubuntu1304"
    },
    'ubuntu1310'=> {
      'define' => :ubuntu1310,
      'box' => "saucy64",
      'url' => "http://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box",
      'name' => "ubuntu1310"
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
      vbox.vm.box_url = param['url']
      vbox.vm.network "public_network"
      vbox.vm.provider :virtualbox do |box|
        box.customize ['modifyvm', :id, '--memory', '1024']
        box.customize ["modifyvm", :id, "--name", param['name'] ]
      end
    end
  end

end
