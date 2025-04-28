# Switch 0


vlan 32
 name WebServers
vlan 42
 name DHCPServers
exit

interface Fa0/10
 switchport mode access
 switchport access vlan 32

interface Fa0/11
 switchport mode access
 switchport access vlan 42


 interface FastEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 32,42


# Multilayer 2

vlan 32
 name WebServers
vlan 42
 name DHCPServers
exit


interface Vlan32
 ip address 192.168.100.1 255.255.255.128
 no shutdown

interface Vlan42
 ip address 192.168.100.129 255.255.255.128
 no shutdown



# Multilayer

interface fa0/14
    no switchport
    ip address 10.0.20.17 255.255.255.252
    no shutdown
exit

interface fa0/13
 no switchport
 ip address 10.0.20.13 255.255.255.252
 no shutdown
exit

ip routing

router ospf 1
 network 10.0.20.16 0.0.0.3 area 0
 network 10.0.20.12 0.0.0.3 area 0
exit



# Router 1

enable
configure terminal


interface g0/0
 ip address 10.0.20.18 255.255.255.252
 no shutdown
exit


interface g0/1.12
 encapsulation dot1Q 12
 ip address 192.168.20.194 255.255.255.240
 ip helper-address 192.168.100.130
 standby 1 ip 192.168.20.193
 standby 1 priority 100
 standby 1 preempt
exit

interface g0/1.22
 encapsulation dot1Q 22
 ip address 192.168.20.2 255.255.255.192
 ip helper-address 192.168.100.130
 standby 2 ip 192.168.20.1
 standby 2 priority 100
 standby 2 preempt
exit

interface g0/1
 no shutdown

router ospf 1
 network 10.0.20.16 0.0.0.3 area 0
exit




# Router 2

interface g0/0
 ip address 10.0.20.14 255.255.255.252
 no shutdown
exit

interface g0/1.12
 encapsulation dot1Q 12
 ip address 192.168.20.194 255.255.255.240
 ip helper-address 192.168.100.130
 standby 1 ip 192.168.20.193
 standby 1 priority 150
 standby 1 preempt
exit

interface g0/1.22
 encapsulation dot1Q 22
 ip address 192.168.20.2 255.255.255.192
 ip helper-address 192.168.100.130
 standby 2 ip 192.168.20.1
 standby 2 priority 150
 standby 2 preempt
exit

interface g0/1
 no shutdown


router ospf 1
 network 10.0.20.12 0.0.0.3 area 0
exit


# Switch

enable
configure terminal

vlan 12
 name ADMIN
exit

vlan 22
 name ESTUDIANTES
exit

interface fa0/10
 switchport mode access
 switchport access vlan 22
exit

interface fa0/11
 switchport mode access
 switchport access vlan 12
exit


interface fa0/1
 switchport mode trunk
exit

interface fa0/2
 switchport mode trunk
exit



---
*Nuevas Configuraciones para el hsrp*
### ROUTER 1 VLAN 22

en
conf t
interface g0/1.12
encapsulation dot1q 12
ip add 192.168.20.2 255.255.255.192
standby 1 ip 192.168.20.1
standby 1 priority 150
standby 1 preempt

### ROUTER 1 VLAN 22

en
conf t
interface g0/1.22
encapsulation dot1q 22
ip add 192.168.20.194 255.255.255.240
standby 2 ip 192.168.20.193
standby 2 priority 150
standby 2 preempt



### ROUTER 2 VLAN 22

en
conf t
interface g0/1.12
encapsulation dot1q 12
ip add 192.168.20.3 255.255.255.192
standby 1 ip 192.168.20.1

### ROUTER 2 VLAN 22
en
conf t
interface g0/1.22
encapsulation dot1q 22
ip add 192.168.20.195 255.255.255.240
standby 2 ip 192.168.20.193


### ROUTER 1 OSPF

router ospf 1
network 10.0.20.16 0.0.0.3 area 0
network 192.168.20.192 0.0.0.15 area 0
network 192.168.20.0 0.0.0.63 area 0


### ROUTER 2 OSPF

router ospf 1
network 10.0.20.12 0.0.0.3 area 0
network 192.168.20.192 0.0.0.15 area 0
network 192.168.20.0 0.0.0.63 area 0