# -*- mode: ruby -*-
# vi: set ft=ruby :

# Interview Tech Test 1

require 'yaml'

Vagrant.configure("2") do |config|

    config.vm.define "ansible" do |ansible|
        ansible.vm.box = "ubuntu/xenial64"
        ansible.vm.hostname = "ansible"
        ansible.vm.network "private_network", ip: "10.75.75.75"

        ansible.vm.provision "shell", inline: "apt-get update"
        ansible.vm.provision "shell", inline: "apt-get install git python-setuptools libssl-dev build-essential autoconf libtool pkg-config python-opengl python-imaging python-pyrex python-pyside.qtopengl idle-python2.7 qt4-dev-tools qt4-designer libqtgui4 libqtcore4 libqt4-xml libqt4-test libqt4-script libqt4-network libqt4-dbus python-qt4 python-qt4-gl libgle3 python-dev -y"
        ansible.vm.provision "shell", inline: "easy_install pip"
        ansible.vm.provision "shell", inline: "pip install setuptools paramiko PyYAML Jinja2 httplib2 six cryptography ansible pywinrm"
    end


    config.vm.define "winweb" do |winweb|
    # Configure and launch the Vagrantbox used for development
        winweb.vm.box = "opentable/win-2012r2-standard-amd64-nocm"
        winweb.vm.hostname = "winweb"
        winweb.vm.network "private_network", ip: "10.75.75.101"
        # winweb.vm.network "forwarded_port", guest: 5985, host: 55985
    end
end
