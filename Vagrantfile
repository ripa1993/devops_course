Vagrant.configure(2) do |config|
# Allow internet connection
config.vm.provider "virtualbox" do |v|
  v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end
# Script for: both
$script = <<-SCRIPT
echo I am provisioning....
echo second time
date > /etc/vagrant_provisioned_at
sudo yum -y update
SCRIPT
# Script for: node1
$script_node1 = <<-SCRIPT
sudo yum -y install ansible
SCRIPT
# Script for: node2
$script_node2 = <<-SCRIPT
sudo yum -y install java git
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum -y install jenkins
sudo service jenkins start
sudo chkconfig jenkins on
SCRIPT
# Define vm node1
  config.vm.define "node1" do |node1|
    node1.vm.box = "bento/centos-7.4"
    node1.vm.network "private_network", ip: "192.168.0.101"
    node1.vm.hostname = "node1"
    node1.vm.provision "shell", inline: $script
    node1.vm.provision "shell", inline: $script_node1
  end
# Define vm node2
  config.vm.define "node2" do |node2|
    node2.vm.box = "bento/centos-7.4"
    node2.vm.network "private_network", ip: "192.168.0.102"
    node2.vm.hostname = "node2"
    node2.vm.provision "shell", inline: $script
    node2.vm.provision "shell", inline: $script_node2
    node2.vm.network "forwarded_port", guest: 8080, host: 9999
  end
end
