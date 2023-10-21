# Code for labwork 2.3.9

## Part 3: Configure and Verify Basic Switch Settings

a. On the Cable Pegboard, click a Console cable. Connect the console cable between S1 and PC-A.

b. Establish a console connection to the switch S1 from PC-A using the Packet Tracer generic Terminal program (PC-A > Desktop > Terminal). Press ENTER to get the Switch> prompt.

c. You can access all switch commands in privileged EXEC mode. The privileged EXEC command set includes those commands contained in user EXEC mode, as well as the configure command through which access to the remaining command modes are gained. Enter privileged EXEC mode by entering the enable command.

```commandline
Switch> enable
Switch#
```

d. The prompt changed from Switch> to Switch# which indicates privileged EXEC mode. Enter global configuration mode.

```commandline
Switch# configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#
```

e. The prompt changed to Switch(config)# to reflect global configuration mode. Give the switch a name according to the Addressing Table.

```commandline
Switch(config)# hostname S1
```
f. Enter local passwords. Use class as the privileged EXEC password and cisco as the password for console access.

```commandline
S1(config)# enable secret class
S1(config)# line con 0
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
```
g. Configure and enable the VLAN 1 interface according to the Addressing Table.

```commandline
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.1 255.255.255.0
S1(config-if)# no shutdown
```

h. A login banner, known as the message of the day (MOTD) banner, should be configured to warn anyone accessing the switch that unauthorized access will not be tolerated. Configure an appropriate MOTD banner to warn about unauthorized access.

```commandline
S1(config)# banner motd #Unauthorized access is strictly prohibited and prosecuted to the full extent of the law.#
S1(config)# exit
```

i. Save the configuration to the startup file on non-volatile random access memory (NVRAM).

```commandline
S1# copy running-config startup-config
Destination filename [startup-config]? [Enter]
Building configuration…
[OK]
S1#
```

j. Display the current configuration.

```commandline
S1# show running-config
Building configuration…
<output omitted>
```

k. Display the IOS version and other useful switch information.

```commandline
S1# show version
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2012 by Cisco Systems, Inc.
Compiled Sat 28-Jul-12 00:29 by prod_rel_team
<output omitted>
```

l. Display the status of the connected interfaces on the switch.

```commandline
S1# show ip interface brief
S1#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual down                  down 
FastEthernet0/3        unassigned      YES manual down                  down 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual up                    up 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
<output omitted>
GigabitEthernet0/1     unassigned      YES manual down                  down 
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  192.168.1.1     YES manual up                    up
S1#
```

m. Repeat the previous steps to configure switch S2. Make sure the hostname is configured as S2.

```commandline
enable
config terminal 
hostname S2
enable secret class
line console 0
password cisco
login
exit
interface vlan 1
ip address 192.168.1.2 255.255.255.0
no shutdown
banner motd #Unauthorized access is strictly prohibited and prosecuted to the full extent of the law.#
end
copy running-config startup-config
```

n. Record the interface status for the following interfaces.

| Interface | S1 Status | S1 Protocol | S2 Status | S2 Protocol |
|-----------|-----------|-------------|-----------|-------------|
| F0/1      | UP        | UP          | UP        | UP          | 
| F0/6      | UP        | UP          | DOWN      | DOWN        |
| F0/18     | DOWN      | DOWN        | UP        | UP          |
| VLAN 1    | UP        | UP          | UP        | UP          |

## Reflection Question

Why are some FastEthernet ports on the switches up while others are down?

<span style="color:yellow">
The FastEthernet ports are up when cables are connected to the ports unless they were manually shutdown by the administrators. Otherwise, the ports would be down.
</span>


What could prevent a ping from being sent between the PCs?

<span style="color:yellow">
Wrong IP address, media disconnected, switch powered off or ports administratively down, firewall.
</span>

