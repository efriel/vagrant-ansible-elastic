Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"  
  config.ssh.insert_key = false
  
  config.vm.provider :kvm do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end


  config.vm.define "elk" do |elk|
    elk.vm.hostname = "elk-app1"
    elk.vm.network :private_network, ip: "172.168.3.25"
    #elk.vm.network :public_network, bridge: 'eth0'
    elk.vm.provision :ansible do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "ansible/inventory"
      ansible.sudo = true
      ansible.ask_sudo_pass = true
    end
    elk.vm.provider :libvirt do |domain|
      domain.memory = 2048
      domain.cpus = 2
    end
  end


  
end
