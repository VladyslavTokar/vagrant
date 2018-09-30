BASE_BOX = "centos/7"
BASE_MEMORY = "512"
APP_SERVERS = 1

Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  config.vm.define :ans do |config|
      config.vm.hostname = "ans"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.10"
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = BASE_MEMORY
      end
      config.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/home/vagrant/.ssh/id_rsa"
      config.vm.provision "shell", inline: "chmod 600 ~/.ssh/id_rsa", privileged: false
      config.vm.provision "shell", inline: "yum install ansible -y"
  end

  config.vm.define :gitlab do |config|
      config.vm.hostname = "gitlab"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.11"
      config.vm.network "forwarded_port", guest: 80, host: 8081
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "1024"
      end
  end

  config.vm.define :jenkins do |config|
      config.vm.hostname = "jenkins"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.12"
      config.vm.network "forwarded_port", guest: 8080, host: 8082
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "1024"
      end
  end

  config.vm.define :nexus do |config|
      config.vm.hostname = "nexus"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.13"
      config.vm.network "forwarded_port", guest: 8081, host: 8083
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "2048"
      end
  end

  config.vm.define :sonar do |config|
      config.vm.hostname = "sonar"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.30"
      config.vm.network "forwarded_port", guest: 9000, host: 8090
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "1024"
      end
  end

  config.vm.define :mysql do |config|
      config.vm.hostname = "mysql"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.31"
      config.vm.network "forwarded_port", guest: 3306, host: 3306
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = BASE_MEMORY
      end
      #mysql root aiR;ai1a
  end

  config.vm.define :docker do |config|
      config.vm.hostname = "docker"
      config.vm.box = BASE_BOX
      config.vm.box_check_update = false
      config.vm.synced_folder "./vagrant", "/vagrant", type: "virtualbox"
      config.vm.network :private_network, ip: "10.0.15.32"
      #config.vm.network "forwarded_port", guest: 80, host: 809x
      config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = BASE_MEMORY
      end
  end

  (1..APP_SERVERS).each do |i|
    config.vm.define :"app#{i}" do |config|
        config.vm.hostname = "app#{i}"
        config.vm.box = BASE_BOX
        config.vm.box_check_update = false
        config.vm.synced_folder ".", "/vagrant", disabled: true
        config.vm.network :private_network, ip: "10.0.15.2#{i}"
        config.vm.provider "virtualbox" do |vb|
          vb.gui = false
          vb.memory = BASE_MEMORY
        end
    end
  end

end
