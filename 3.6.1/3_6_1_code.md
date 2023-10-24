# Code for labwork 3.6.1

## Part 1: Configure VLANs
### Switch A / Switch B / Switch C

```commandline
enable
configure terminal
vlan 10
name Admin
vlan 20
name Accounts
vlan 30
name HR
vlan 40
name Voice
vlan 99
name Management
vlan 100
name Native
```

## Part 2: Assign Ports to VLANs

### Step 1: Assign access ports to VLANs

### Switch B

```commandline
interface f0/1
switchport mode access
switchport access vlan 10
interface f0/2
switchport mode access
switchport access vlan 20
interface f0/3
switchport mode access
switchport access vlan 30
```

### Switch C

```commandline
interface f0/1
switchport mode access
switchport access vlan 10
interface f0/2
switchport mode access
switchport access vlan 20
interface f0/3
switchport mode access
switchport access vlan 30
interface f0/4
switchport mode access
switchport access vlan 10
```

### Step 2: Configure the Voice VLAN port

### Switch C

```commandline
interface f0/4
mls qos trust cos
switchport voice vlan 40
```

### Step 3: Configure the virtual management interfaces

c. The switches should not be able to ping each other

### Switch A
```commandline
SWA(config)#interface vlan 99
SWA(config-if)#ip address 192.168.99.252 255.255.255.0
SWA(config-if)#no shutdown
```

### Switch B

```commandline
SWB(config)#interface vlan 99
SWB(config-if)#ip address 192.168.99.253 255.255.255.0
SWB(config-if)#no shutdown
```

### Switch C

```commandline
SWC(config)#interface vlan 99
SWC(config-if)#ip address 192.168.99.254 255.255.255.0
SWC(config-if)#no shutdown
```
## Part 3: Configure Static Trunking
a. Configure the link between SWA and SWB as a static trunk. Disable dynamic trunking on this port.

b. Disable DTP on the switch port on both ends of the trunk link.

c. Configure the trunk with the native VLAN and eliminate native VLAN conflicts if any.

### Switch A

```commandline
SWA(config)#interface g0/1
SWA(config-if)#switchport mode trunk
SWA(config-if)#switchport nonegotiate
SWA(config-if)#switchport trunk native vlan 100
```

### Switch B

```commandline
SWB(config)#interface g0/1
SWB(config-if)#switchport mode trunk
SWB(config-if)#switchport nonegotiate
SWB(config-if)#switchport trunk native vlan 100
```

## Part 4: Configure Dynamic Trunking

### Switch A
```commandline
SWA(config)#interface g0/2
SWA(config-if)#switchport mode dynamic desirable
SWA(config-if)#switchport trunk native vlan 100
```

### Switch C
```commandline
SWC(config)#interface g0/2
SWC(config-if)#switchport mode trunk
SWC(config-if)#switchport trunk native vlan 100
```

## Answer Scripts

### Switch SWA

```commandline
enable
conf t
vlan 10
 name Admin
vlan 20
 name Accounts
vlan 30
 name HR
vlan 40
 name Voice
vlan 99
 name Management
vlan 100
 name Native
interface GigabitEthernet0/1
 switchport trunk native vlan 100
 switchport mode trunk
 switchport nonegotiate
interface GigabitEthernet0/2
 switchport trunk native vlan 100
 switchport mode dynamic desirable
interface Vlan1
 no ip address
 shutdown
interface Vlan99
ip address 192.168.99.252 255.255.255.0
end
```

### Switch SWB

```commandline
enable
conf t
vlan 10
 name Admin
vlan 20
 name Accounts
vlan 30
 name HR
vlan 40
 name Voice
vlan 99
 name Management
vlan 100
 name Native
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access
interface FastEthernet0/3
 switchport access vlan 30
 switchport mode access
interface GigabitEthernet0/1
 switchport trunk native vlan 100
 switchport mode trunk
 switchport nonegotiate
interface Vlan99
ip address 192.168.99.253 255.255.255.0
end
```

### Switch SWC

```commandline
enable
conf t
vlan 10
 name Admin
vlan 20
 name Accounts
vlan 30
 name HR
vlan 40
 name Voice
vlan 99
 name Management
vlan 100
 name Native
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access
interface FastEthernet0/3
 switchport access vlan 30
 switchport mode access
interface FastEthernet0/4
 switchport access vlan 10
 switchport mode access
 switchport voice vlan 40
 mls qos trust cos
interface GigabitEthernet0/2
 switchport trunk native vlan 100
 switchport mode trunk
interface Vlan99
ip address 192.168.99.254 255.255.255.0
end
```

