VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "netatalk.yml"
    ansible.sudo = true
  end

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

end
