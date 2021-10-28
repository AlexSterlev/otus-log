Vagrant.configure("2") do |config|

    config.vm.define "log" do |log|
      log.vm.network "private_network", ip: "192.168.11.151"
      log.vm.hostname = "log"
      log.vm.define "log"
      log.vm.box_download_insecure = true
      log.vm.box = "centos/7"
      log.vm.provider "virtualbox" do |vb2|
        vb2.memory = "2048"
    
      end
    log.vm.provision "shell", path: "log.sh"  
    end
  
    config.vm.define "web" do |web|
      web.vm.network "private_network", ip: "192.168.11.150"
      web.vm.hostname = "web"
      web.vm.define "web"
      web.vm.box_download_insecure = true
      web.vm.box = "centos/7"
      web.vm.provider "virtualbox" do |vb1|
        vb1.memory = "2048"
      end
    web.vm.provision "shell", path: "web.sh"
    end
    
  end
