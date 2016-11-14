# apiteam-season2-workshop-vagrant

## Prerequisites  

* Install VirtualBox and Vagrant  
VirtualBox: <https://www.virtualbox.org/>  
Vagrant: <https://www.vagrantup.com/>  
NOTICE: Just now, you should use VirtualBox ver.5.0.x
https://www.virtualbox.org/wiki/Download_Old_Builds_5_0
NOTICE: Just now, you should use vagrant ver. 1.7.4  
https://releases.hashicorp.com/vagrant/1.7.4/
* Get apigee-edge-4.15.07.03.zip and save it in the same directory as the playbook(../apiteam-season2-workshop-apigw-allinone)
* Save a valid license file for Apigee Edge in the same directory as the playbook(../apiteam-season2-workshop-apigw-allinone)


## Getting Started
```
#git clone this repo
git clone https://github.com/YasuhideKato/apiteam-season2-workshop-vagrant.git

#git clone ansible-playbook for apigw silent install
git clone https://github.com/YasuhideKato/apiteam-season2-workshop-apigw-allinone.git

#box dl
vagrant box add centos66 https://dl.dropbox.com/s/yr5xbz177heaav2/centos66.box

#VMs launch
vagrant up

#VMs check
vagrant status

#check
vagrant ssh jump
vagrant ssh edge
vagrant ssh baas

#VM stop
vagrant halt VM_NAME

#VM delete
vagrant destroy VM_NAME
```
## Next Action
https://github.com/YasuhideKato/apiteam-season2-workshop-apigw-allinone

## Others
TBD
