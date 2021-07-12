# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "breeze/win7-ie11"
  config.vm.guest = "windows"
  config.ssh.username = "IEUser"
  config.ssh.password = "Passw0rd!"
  config.ssh.insert_key = false
  config.ssh.shell = 'sh -l'
  config.ssh.sudo_command = ''
  # config.vm.synced_folder "./vagrant", "c:\\vagrant", create:"true"
  config.vm.provider "virtualbox" do |v|
    v.gui = true
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
    v.customize ["modifyvm", :id, "--memory", mem]

    # v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end
end
