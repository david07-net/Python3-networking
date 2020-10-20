# Introduction 
This is a tutorial on how to connect to a single cisco switch. For this tutorial we are using the library knows at [Netmiko](https://github.com/ktbyers/netmiko). Please feel free to go in the link for more information. 

## Requirements

1. Have Python3 and Netmiko install. 
2. We well need to configure manually the following parameters: SSH connection, username, password, mangement IP address. 

### Configuration on the Cisco Device

```
enable
configure terminal
hostname SW1
ip domain-name practice.com
enable secret cisco
username david secret cisco
interface vlan 1
description MGMT_VLAN
ip address 192.168.1.11 255.255.255.0
no shutdown
ip default-gateway 192.168.1.1
line vty 0 4
transport input ssh
login local
exit
write memory
```




