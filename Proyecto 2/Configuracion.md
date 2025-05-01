
# Configuracion switch, multilayer

## Switch
```bash
interface range Fa0/5 - 7
switchport mode trunk
switchport trunk allowed vlan all
channel-protocol lacp
channel-group 1 mode active
no shutdown


interface range fa0/1-2
no switchport mode access
no switchport access vlan 10
```

## multilayer
```bash
interface range Fa0/5 - 7
switchport mode trunk
switchport trunk allowed vlan all
channel-protocol lacp
channel-group 1 mode active
no shutdown

interface range fastEthernet0/1-4
no sh
exit

```

## ML Switch 7(centro)
```bash 
conf t

ip routing
interface GigabitEthernet 1/1/2
 no switchport
 ip address 172.20.0.1 255.255.255.252
 no shutdown
 exit

interface GigabitEthernet 1/1/1
 no switchport
 ip address 172.20.0.5 255.255.255.252
 no shutdown
 exit

interface GigabitEthernet 1/0/1
no switchport
ip address 192.168.12.42 255.255.255.252
no sh
exit

router bgp 100
 bgp log-neighbor-changes
 no synchronization
 neighbor 172.20.0.2 remote-as 200
 neighbor 172.20.0.6 remote-as 300
 network 172.20.0.2 mask 255.255.255.252
 network 172.20.0.4 mask 255.255.255.252
 network 192.168.12.40 mask 255.255.255.252
 redistribute eigrp 1
 exit


router eigrp 1       
redistribute bgp 100 metric 10000 100 255 1 1500
network 192.168.12.40 0.0.0.3
no auto-summary   
exit

 

```

## ML Switch 8(centro)
```bash 
conf t

ip routing
interface GigabitEthernet 1/1/1
 no switchport
 ip address 172.20.0.6 255.255.255.252
 no shutdown
 exit

interface GigabitEthernet 1/1/2
 no switchport
 ip address 172.20.0.10 255.255.255.252
 no shutdown
 exit

interface GigabitEthernet 1/0/24
 no switchport
 ip address 192.168.32.69 255.255.255.252
 no shutdown
 exit

router bgp 300
 bgp log-neighbor-changes
 no synchronization
 redistribute ospf 20
 neighbor 172.20.0.1 remote-as 100
 neighbor 172.20.0.9 remote-as 200
 network 172.20.0.0 mask 255.255.255.252
 network 172.20.0.8 mask 255.255.255.252
 network 192.168.32.68 mask 255.255.255.252 
 exit

router ospf 20
 log-adjacency-changes
 redistribute bgp 300 subnets
 network 192.168.32.68 0.0.0.3 area 0
 exit
 

```

## ML Switch 6
```bash
interface GigabitEthernet 1/0/24
 no switchport
 ip address 192.168.32.70 255.255.255.252
 no shutdown
 exit

router ospf 20
 log-adjacency-changes
 network 192.168.32.60 0.0.0.3 area 0
 network 192.168.32.64 0.0.0.3 area 0
 network 192.168.32.68 0.0.0.3 area 0 #subred del router red autonomo la que conectan los routers

 
 

 
```


## ML Switch 9(centro)
```bash 
conf t

ip routing
interface GigabitEthernet 1/1/1
 no switchport
 ip address 172.20.0.2 255.255.255.252
 no shutdown
 exit

interface GigabitEthernet 1/1/2
 no switchport
 ip address 172.20.0.9 255.255.255.252
 no shutdown
 exit


router bgp 200
 bgp log-neighbor-changes
 no synchronization
 neighbor 172.20.0.1 remote-as 100
 neighbor 172.20.0.10 remote-as 300
 network 172.20.0.0 mask 255.255.255.252
 network 172.20.0.8 mask 255.255.255.252
 network 192.168.32.68 mask 255.255.255.252



```

## Router0

```bash
interface fastethernet 1/0
ip address 192.168.12.1 255.255.255.248
ip helper-address 192.168.12.38
no sh
exit

interface fastethernet 3/0
ip address 192.168.12.9 255.255.255.248
ip helper-address 192.168.12.38
no sh
exit


interface fastethernet 4/0
ip address 192.168.12.17 255.255.255.248
ip helper-address 192.168.12.38
no sh
exit

interface fastethernet 2/0
ip address 192.168.12.25 255.255.255.248
ip helper-address 192.168.12.38
no sh
exit



interface fastethernet 0/0
ip address 192.168.12.33 255.255.255.252
no sh
exit

interface fastethernet 5/0
ip address 192.168.12.41 255.255.255.252
no sh
exit

router eigrp 1       
network 192.168.12.0 0.0.0.7   
network 192.168.12.8 0.0.0.7  
network 192.168.12.16 0.0.0.7   
network 192.168.12.24 0.0.0.7  
network 192.168.12.32 0.0.0.3 
network 192.168.12.40 0.0.0.3
no auto-summary   
exit







```

## Router1

```bash
Interface fa1/0
ip address 192.168.12.37 255.255.255.252
no sh
exit

interface fastethernet 0/0
ip address 192.168.12.34 255.255.255.252
no sh
exit


router eigrp 1          
network 192.168.12.32 0.0.0.3 
no auto-summary    
exit



```


# Vlans

``` bash
vlan 10
name "AtencionAlCliente"
vlan 20
name "Administracion"
```



