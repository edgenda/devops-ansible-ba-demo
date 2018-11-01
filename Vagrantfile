Vagrant.configure("2") do |config|
  
  (1..3).each do |i|
    config.vm.define "host0#{i}" do |host|
      host.vm.box = "centos/7"
      host.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"
      host.vm.network "private_network", ip: "192.168.10.#{i}"
      case i
      when 1
        host.vm.network "forwarded_port", guest: 8008, host: 8008
        host.vm.network "forwarded_port", guest: 8009, host: 8009
      when 2
        host.vm.network "forwarded_port", guest: 8080, host: 8080
      when 3
        host.vm.network "forwarded_port", guest: 8081, host: 8081
      end

      (1..4).each do |i|
        host.vm.provision "shell", inline: <<-SHELL
          sed -i '$ a 192.168.10.#{i} host0#{i}' /etc/hosts
        SHELL
      end
    end
  end

  config.vm.define "host04" do |host|
    host.vm.box = "ubuntu/trusty64"
    host.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"
    host.vm.network "private_network", ip: "192.168.10.4"
    (1..4).each do |i|
      host.vm.provision "shell", inline: <<-SHELL
        sed -i '$ a 192.168.10.#{i} host0#{i}' /etc/hosts
      SHELL
    end
  end

end