Vagrant.configure("2") do |config|
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 1
  end

  config.vm.define "dc" do |dc|
    dc.vm.guest = :windows
    dc.vm.communicator = "winrm"
    dc.vm.boot_timeout = 600
    dc.vm.graceful_halt_timeout = 600
    dc.winrm.retry_limit = 30
    dc.winrm.retry_delay = 10
    dc.vm.box = "ws"
    dc.vm.network "private_network", ip: "192.168.56.10"
    dc.vm.network :forwarded_port, guest: 3389, host: 23389, id: "msrdp"
    dc.vm.network :forwarded_port, guest: 5985, host: 25985, id: "winrm"
    dc.vm.provision "shell", path:"ConfigureRemotingForAnsible.ps1"
  end


  config.vm.define "win_workstation" do |win_workstation|
    win_workstation.vm.guest = :windows
    win_workstation.vm.communicator = "winrm"
    win_workstation.vm.boot_timeout = 600
    win_workstation.vm.graceful_halt_timeout = 600
    win_workstation.winrm.retry_limit = 30
    win_workstation.winrm.retry_delay = 10    
    win_workstation.vm.box = "win"
    win_workstation.vm.network "private_network", ip: "192.168.56.12"
    win_workstation.vm.network :forwarded_port, guest: 3389, host: 43389, id: "msrdp"
    win_workstation.vm.network :forwarded_port, guest: 5985, host: 45985, id: "winrm"
    win_workstation.vm.provision "shell", path:"ConfigureRemotingForAnsible.ps1"
  end

  config.vm.define "ubuntu_domain" do |ubuntu_domain|
    ubuntu_domain.vm.box = "ubuntu"
    ubuntu_domain.vm.network "private_network", ip: "192.168.56.13"
    ubuntu_domain.vm.network :forwarded_port, guest: 22, host: 10022, id: "msrdp"
  end


end
