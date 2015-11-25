boxes = [ "mesos-master1", "mesos-master2", "mesos-master3", "mesos-slave1", "mesos-slave2", "mesos-slave3" ]

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.network "private_network", type: "dhcp", :adapter => 2
  
  config.vm.provider :virtualbox do |v|
	v.memory = 3072
	v.cpus = 2
  end
  
  boxes.each do |box|
	config.vm.define box do |config|
		config.vm.hostname = box
		if box == boxes.last
			config.vm.provision :ansible do |ansible|
				ansible.playbook = "mesos.yml"
				ansible.sudo = true
				ansible.limit = "all"
				ansible.groups = {
					"master" => ["mesos-master1", "mesos-master2", "mesos-master3"],
					"slave" => ["mesos-slave1", "mesos-slave2", "mesos-slave3"]
				}
			end
		end
	end
  end
end
