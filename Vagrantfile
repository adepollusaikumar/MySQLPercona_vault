$script = <<-'SCRIPT'
echo "Installing pre-requisites"
sudo bash -c 'apt-get update -y >/dev/null 2>&1 ' 
sudo bash -c 'apt-get install docker  docker-compose -y >/dev/null 2>&1 '
sudo bash -c 'docker-compose  -f /vagrant/docker-compose.yml up -d  >/dev/null 2>&1 '
SCRIPT

Vagrant.configure("2") do |config|
       config.vm.box = "bento/ubuntu-20.04"
       config.ssh.insert_key = false
       config.hostmanager.enabled = true
       config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
       config.vm.provider "virtualbox" do |vb|
     vb.customize ["modifyvm", :id, "--memory", 2048]
     vb.customize ["modifyvm", :id, "--cpus", 4]
 end

  (  ["PERCONAVAULT"] ).each_with_index do |role, i|
    name = "%s"     % [role, i]
    addr = "10.0.12.%d" % (100 + i)
    config.vm.define name do |node|
      node.vm.hostname = name
      node.vm.network "private_network",ip: addr
      node.vm.provision "shell", inline: $script
        end
    end

end
