VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
echo 'Start ShellScript'
sudo yum install ntp -y
sudo service ntpd start
sudo chkconfig ntpd on
sudo service iptables stop
sudo chkconfig iptables off
sudo rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
sudo yum install ansible -y
SCRIPT

#$script1= <<SCRIPT1
#echo 'Start ShellScript for jump'
#mkdir -p module && cd module
#if [ ! -d "apigee-all-in-one" ]; then
#  git clone https://github.com/mozzio/apigee-all-in-one.git
#fi
#SCRIPT1

$jump_host = <<JUMP
echo "127.0.0.1 localhost\n::1      localhost\n192.168.33.5    jump" > /etc/hosts
JUMP

$edge_host = <<EDGE
echo "127.0.0.1 localhost\n::1      localhost\n192.168.33.10    edge" > /etc/hosts
EDGE

$baas_host = <<BAAS
echo "127.0.0.1 localhost\n::1      localhost\n192.168.33.20    baas" > /etc/hosts
BAAS

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.insert_key = false

  config.vm.define "jump" do |jump|
    jump.vm.box = "centos66" 
    jump.vm.network "private_network", ip: "192.168.33.5"
    jump.vm.hostname = "jump"
    jump.vm.synced_folder "../apigw_module", "/vagrant", mount_options: ['dmode=775','fmode=775']
    jump.vm.provision "shell", inline: $jump_host
    jump.vm.provision "shell", inline: $script
    #jump.vm.provision "shell", inline: $script1
  end

  config.vm.define "edge" do |edge|
    edge.vm.box = "centos66" 
    edge.vm.network "private_network", ip: "192.168.33.10"
    edge.vm.hostname = "edge"
    edge.vm.synced_folder "../apigw_module", "/vagrant", mount_options: ['dmode=775','fmode=775']
    edge.vm.provision "shell", inline: $edge_host
    edge.vm.provision "shell", inline: $script
  end

  config.vm.define "baas" do |baas|
    baas.vm.box = "centos66"
    baas.vm.network "private_network", ip: "192.168.33.20"
    baas.vm.hostname = "baas"
    baas.vm.synced_folder "../apigw_module", "/vagrant", mount_options: ['dmode=775','fmode=775']
    baas.vm.provision "shell", inline: $baas_host
    baas.vm.provision "shell", inline: $script
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["setextradata", :id,  "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 0]
    vb.customize ["modifyvm", :id, "--memory", "1536"]
  end

end
