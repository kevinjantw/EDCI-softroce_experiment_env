# EDCI-SoftRoCE_Experiment_Env
Build SoftRoCE Experiment Environment on VirtualBox VMs

## Contact
kevinjan@iii.org.tw 

## Install VirtualBox and Vargant
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads) - A desktop virtualization system.
* [Vagrant](https://www.vagrantup.com/downloads.html) - A script tool for managing VirtualBox VMs.

## Reference source code for building VM and SoftRoCE packages
Download and unzip the rdma-experiment source code to directory "rdma-experiment-master".  
https://github.com/haggaie/rdma-experiment

## Vagrant script for building two VMs
Original Vagrant script only builds one SoftRoCE VM.   
Edit the file "Vagrantfile" under directory "rdma-experiment-master" to build two SoftRoCE VMs.
```shell=
# Build SoftRoCE Server and SoftRoCE Client
Vagrant.configure("2") do |config|
    
  config.vm.define "softroce_server" do |softroce_server|    
    softroce_server.vm.box = "ubuntu/bionic64"
    softroce_server.vm.network "private_network", type: "dhcp"
    softroce_server.vm.provision "shell", path: "provision/setup-vm.sh"    
  end
  
  config.vm.define "softroce_client" do |softroce_client|    
    softroce_client.vm.box = "ubuntu/bionic64"
    softroce_client.vm.network "private_network", type: "dhcp"
    softroce_client.vm.provision "shell", path: "provision/setup-vm.sh"    
  end
  
end
```

## Run Vagrant script to build SoftRoCE Server VM and SoftRoCE Client VM
```shell=
cd rdma-experiment-master
vagrant up
```
The command "vagrant up" will take a lot of time to build two SoftRoCE VMs.

## SSH login SoftRoCE Server VM
```shell=
vagrant ssh softroce_server
```

## SSH login SoftRoCE Client VM
```shell=
vagrant ssh softroce_client
```

## How to configure SoftRoCE and test SoftRoCE communication
https://www.systutorials.com/docs/linux/man/8-rxe_cfg/  
https://zhengjingwei.github.io/2018/01/27/Soft-RoCE-setup/

## References
http://syswift.com/458.html

