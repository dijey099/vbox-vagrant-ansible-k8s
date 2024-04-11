# Wroten by Dijey (2024)

IMAGE_NAME = "ubuntu/focal64"

NETWORK_BASE = "192.168.56."

MASTER_CPU = 2
MASTER_RAM = 2048

WORKERS = 1
WORKERS_CPU = 1
WORKERS_RAM = 2048

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
      
    config.vm.define "srv-k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.provider "virtualbox" do |vb|
            vb.memory = MASTER_RAM
            vb.cpus = MASTER_CPU
	    vb.gui = true
        end
        master.vm.network "private_network", ip: "#{NETWORK_BASE}10"
        master.vm.hostname = "srv-k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "master.yml"
        end
    end

    (1..WORKERS).each do |i|
        config.vm.define "srv-k8s-worker#{i}" do |worker|
            worker.vm.box = IMAGE_NAME
            worker.vm.provider "virtualbox" do |vb|
                vb.memory = WORKERS_RAM
                vb.cpus = WORKERS_CPU
		vb.gui = true
            end
            worker.vm.network "private_network", ip: "#{NETWORK_BASE}#{10 + i}"
            worker.vm.hostname = "srv-k8s-worker#{i}"
            worker.vm.provision "ansible" do |ansible|
                ansible.playbook = "workers.yml"
            end
        end
    end
end

