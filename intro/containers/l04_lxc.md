#lxc uses namespaces and control groups

apt install lxd lxd-client

lxd init

lxc launch ubuntu:16.04



does not work in docker dev image
https://bobcares.com/blog/lxc-container-config/

apt-get install lxc lxc-templates -y
lxc-checkconfig
ls /usr/share/lxc/templates/
lxc-create -n new-container -t ubuntu
