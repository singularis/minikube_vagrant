$script = <<-SCRIPT
echo "I am provisioning..."
sudo yum install git curl vim wget bash-completion docker -y
git clone https://github.com/singularis/ckad.git
cd ckad
chmod +x kube-setup.sh
sudo ./kube-setup.sh
SCRIPT

Vagrant.configure("2") do |config|
	config.vm.network "private_network", ip: "192.168.50.5"
	config.vm.provision "shell", inline: $script
	config.vm.define "k8s-box" do |k8s|
		k8s.vm.hostname = "k"
		k8s.vm.box = "generic/fedora33"
		k8s.vm.provider :virtualbox
		k8s.vm.disk :disk, size: "40GB", primary: true
		k8s.vm.provider "virtualbox" do |v|
			v.customize ["modifyvm", :id, "--nested-hw-virt", "on"]
    			v.memory = 8192
    			v.cpus = 4
    		end
	end
end
