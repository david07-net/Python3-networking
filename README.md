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

##  Python Script

```Python

# We import a module from netmiko

from netmiko import ConnectHandler

# Create a dictionary representing the cisco device. 

iosv_l2 = {
    'device_type': 'cisco_ios',
    'ip': '192.168.1.11',
    'username': 'david',
    'password': 'cisco',
    'port': 22,         # Default value is 22
    'secret': 'cisco'   # Default value is ''
}

# Establish an SSH connection to the device by passing in the device dictionary.

net_connect = ConnectHandler(**iosv_l2)

#Execute the command to show IP address info on the switch

output = net_connect.send_command('show ip int brief')
print (output)

#Execute the command to show vlan information

output = net_connect.send_command('show vlan brief')
print (output)

#Execute the command to show interface trunk information

output = net_connect.send_command('show interface trunk')
print (output)
```

With a single program we are able to run multiple cisco commands and get information we need about the cisco switch. There can be more commands of course.



