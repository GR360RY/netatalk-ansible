VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "netatalk.yml"
    ansible.sudo = true
  end

  config.vm.define "ubuntu1204" do |ubuntu1204|
    config.vm.network "public_network"
    ubuntu1204.vm.provider :virtualbox do |vbox|
      vbox.customize ['modifyvm', :id, '--memory', '1024']
    end
  end

end
