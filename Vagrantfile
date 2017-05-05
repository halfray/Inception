# -*- mode: ruby -*-
# vi: set ft=ruby :

$cluster_guest = {name: 'cluster-guest',ip: '192.168.42.10'}
$cluster_host_list = [
	{name: 'cluster-master',ip: '192.168.42.11',memory: 5400},
	{name: 'cluster-slave1',ip: '192.168.42.12',memory: 3072},
	{name: 'cluster-slave2',ip: '192.168.42.13',memory: 3072}]
Vagrant.configure("2") do |config|
  config.vm.box = "centos/6.9"
  
  #  set cluster vm
  $cluster_host_list.each_with_index do |host|
  	config.vm.define host[:name] do |config|
  		config.vm.synced_folder ".", "/vagrant", disabled: true
		config.vm.network "private_network", ip: host[:ip] 
		config.vm.provider "virtualbox" do |v|
		  v.memory = host[:memory] 
		end
  	end
  end

# set guest vm
  config.vm.define $cluster_guest[:name], primary: true do |config|
        config.vm.synced_folder ".", "/vagrant"
	config.vm.network "private_network", ip: $cluster_guest[:ip] 
	# run ansible playbook
	config.vm.provision "ansible_local" do |ansible|
    		ansible.playbook = "playbook.yml"
		ansible.inventory_path = "hosts"
		ansible.limit = 'all'
		ansible.raw_arguments  = [
		  "-e hadoop_user=root",
		  "-e hadoop_group=root",
		  # password must encrypt: python -c 'import crypt; print crypt.crypt("your password", "$1$SomeSalt$")'
		  # must use ' not "
		  # muse use \$  not $
		  '-e hadoop_user_passwd=\$1\$SomeSalt\$7Tc/nAZ6FDAOoef4j0HYw1', 
		  "-e master=master"
		]
		ansible.install  = true
  	end
  end

end
