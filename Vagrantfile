# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.customize ["modifyvm", :id, "--vram", "64"]
  end

$provision = <<-SCRIPT
  reflector --latest 5 --sort rate --save /etc/pacman.d/mirrorlist
  pacman --noconfirm -R virtualbox-guest-utils-nox
  pacman --noconfirm -Syyu
  pacman --noconfirm -S virtualbox-guest-utils xf86-video-vmware xorg xfce4 xfce4-goodies lightdm lightdm-gtk-greeter python-yaml python-owslib python-psycopg2 python-jinja python-gdal python-pygments ttf-{liberation,dejavu,hack} qgis
  systemctl enable vboxservice
  systemctl start vboxservice
  systemctl enable lightdm
  systemctl set-default graphical.target
  systemctl isolate graphical.target
SCRIPT

  config.vm.provision "shell", inline: $provision

end
