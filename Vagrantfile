# -*- mode: ruby -*-
# vi: set ft=ruby :

%w(vagrant-hostmanager vagrant-auto_network).each do |plugin|
 unless Vagrant.has_plugin?(plugin)
   raise 'In order to use this box, you must install plugin: ' + plugin
 end
end

Vagrant.configure("2") do |config|


    config.vm.box = "creatuity/MageScotchBox"
    config.vm.box_version = ">= 2.0.8"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.provision "fix-no-tty", type: "shell" do |s|
    	s.privileged = false
    	s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
    end

    config.vm.provision :shell, path: "bootstrap.sh"
    config.vm.hostname = "magescotch"
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.synced_folder "./", "/var/www", type:"nfs", mount_options:["nolock,vers=3,udp,noatime,actimeo=1"] 

  host = RbConfig::CONFIG['host_os']

  # Give VM 1/4 system memory 
  if host =~ /darwin/
    # sysctl returns Bytes and we need to convert to MB
    mem = `sysctl -n hw.memsize`.to_i / 1024
  elsif host =~ /linux/
    # meminfo shows KB and we need to convert to MB
    mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i 
  elsif host =~ /mswin|mingw|cygwin/
    # Windows code via https://github.com/rdsubhas/vagrant-faster
    mem = `wmic computersystem Get TotalPhysicalMemory`.split[1].to_i / 1024
  end

  mem = mem / 1024 / 4
    config.vm.provider "virtualbox" do |v|
  	v.cpus = 2
        v.customize ["modifyvm", :id, "--memory", mem]
    end



    config.ssh.forward_agent = true

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

end
