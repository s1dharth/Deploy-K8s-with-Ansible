ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
Vagrant.require_version ">= 1.7.0"
Vagrant.configure(2) do |config|
	(1..3).each do |i|
		config.vm.define "node-#{i}" do |node|
			# Identify which Vagrant box to use
			node.vm.box = "centos/7"
			# Define host settings
			node.vm.hostname = "node-#{i}.example.com"
			node.vm.box_check_update = false
			# Define sync folder(s)
			# Define shell provisioner
			#node.vm.provision "shell", path: "provisioner.sh"
			# Define ansible provisioner
			node.vm.provision "ansible" do |ansible|
				ansible.playbook = "test.yml"
			end
			node.vm.network "forwarded_port", guest: 80, host: 8000
			# Define ansible provisioner
			node.vm.provider :libvirt do |domain|
				domain.driver = "kvm"
      				domain.memory = 512
				domain.nested = true
				domain.storage :file, :size => '20G'
			end
		end
	end
end
