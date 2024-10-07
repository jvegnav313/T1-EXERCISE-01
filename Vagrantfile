Vagrant.configure("2") do |config|

  config.vm.box = "debian/bookworm64"

  config.vm.provider "virtualbox"  do |vb|
  
    vb.memory = 512
  
  end

  config.vm.define "server" do |server|

    server.vm.network "private_network", ip: "192.168.56.10"
    server.vm.network "private_network", 
      ip: "192.168.57.10", 
      virtualbox__intnet: true

    server.vm.provision "shell",
    inline: <<-SHELL
    apt update && upgrade -y
    apt install -y isc-dhcp-server
    cp -f /vagrant/dhcpd.conf /etc/dhcp/
    cp -f /vagrant/isc-dhcp-server /etc/default/
    systemctl restart isc-dhcp-server.service
    SHELL
  end

  
  config.vm.define "c1" do |c1|

    c1.vm.network "private_network", type: "dhcp",
      virtualbox__intnet: true 

  end

  config.vm.define "c2" do |c2|

    c2.vm.network "private_network", type: "dhcp",
    mac:"aaaaaa010101",
    virtualbox__intnet: true

  end

end