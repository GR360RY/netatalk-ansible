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
    }
  }

  machines.each do |os,param|
    config.vm.define param['define'] do |vbox|
      # Ubuntu Server 12.04 amd64 Minimal from files.vagrantup.com
      vbox.vm.provision "ansible" do |ansible|
        ansible.playbook = "netatalk.yml"
        ansible.extra_vars = { vm_hostname: param['name'] }
        ansible.sudo = true
      end
      vbox.vm.box = param['box']
      vbox.vm.box_url = param['url']
      vbox.vm.network "public_network"
      vbox.vm.provider :virtualbox do |box|
        box.customize ['modifyvm', :id, '--memory', '1024']
        box.customize ["modifyvm", :id, "--name", param['name'] ]
      end
    end
  end

end
