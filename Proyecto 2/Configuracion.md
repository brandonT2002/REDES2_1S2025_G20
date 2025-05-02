
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
 neighbor 172.20.0.1 remote-as 100
 neighbor 172.20.0.9 remote-as 200
 network 172.20.0.0 mask 255.255.255.252
 network 172.20.0.8 mask 255.255.255.252
 network 192.168.32.68 mask 255.255.255.252 
redistribute ospf 20
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
 network 192.168.22.128 mask 255.255.255.252
 redistribute eigrp 4


router eigrp 4    
redistribute bgp 200 metric 10000 100 255 1 1500
network 192.168.22.128 0.0.0.3
no auto-summary   
exit

interface Gi1/0/7
no switchport
ip address 192.168.22.130 255.255.255.252
no sh
exit

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

# Configuración ISP2: Redes Nacionales

Subnetting: 

> Red Pricipal: 192.168.22.0/24

|Nombre|Hosts|ID Red|Primera IP Utilizable|Última IP Utilizable|Broadcast|Máscara de Subred|
|-|-|-|-|-|-|-|
|Ventas1|14|192.168.22.0|192.168.22.1|192.168.22.14|192.168.22.15|255.255.255.240/28|
|Ventas2|14|192.168.22.16|192.168.22.17|192.168.22.30|192.168.22.31|255.255.255.240/28|
|Facturacion1|14|192.168.22.32|192.168.22.33|192.168.22.46|192.168.22.47|255.255.255.240/28|
|Facturacion2|14|192.168.22.48|192.168.22.49|192.168.22.62|192.168.22.63|255.255.255.240/28|
|Wireless1|14|192.168.22.64|192.168.22.65|192.168.22.78|192.168.22.79|255.255.255.240/28|
|Wireless2|14|192.168.22.80|192.168.22.81|192.168.22.94|192.168.22.95|255.255.255.240/28|
||2|192.168.22.96|192.168.22.97|192.168.22.98|192.168.22.99|255.255.255.252/30|
||2|192.168.22.100|192.168.22.101|192.168.22.102|192.168.22.103|255.255.255.252/30|
||2|192.168.22.104|192.168.22.105|192.168.22.106|192.168.22.107|255.255.255.252/30|
||2|192.168.22.108|192.168.22.109|192.168.22.110|192.168.22.111|255.255.255.252/30|
||2|192.168.22.112|192.168.22.113|192.168.22.114|192.168.22.115|255.255.255.252/30|
||2|192.168.22.116|192.168.22.117|192.168.22.118|192.168.22.119|255.255.255.252/30|
||2|192.168.22.120|192.168.22.121|192.168.22.122|192.168.22.123|255.255.255.252/30|
||2|192.168.22.124|192.168.22.125|192.168.22.126|192.168.22.127|255.255.255.252/30|
||2|192.168.22.128|192.168.22.129|192.168.22.130|192.168.22.131|255.255.255.252/30|

Enrutamiento
Interfaces

* SW4
    * LACP: Gi1/0/1-3 - Port-Channel1
    * LACP: Gi1/0/4-6 - Port-Channel2

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|Gi1/0/1|192.168.22.97|255.255.255.252/30|
|Gi1/0/2|||
|Gi1/0/3|||
|Gi1/0/4|192.168.22.101|255.255.255.252/30|
|Gi1/0/5|||
|Gi1/0/6|||

* SW2
    * LACP Gi1/0/1-3 - Port-Channel1

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|Gi1/0/1|192.168.22.98|255.255.255.252/30|
|Gi1/0/2|||
|Gi1/0/3|||

* SW3
    * LACP G1/0/4-6 - Port-Channel2

|Interfaz|IP|Máscara de Subred|
|-|-|-|
|Gi1/0/4|192.168.22.102|255.255.255.252/30|
|Gi1/0/5|||
|Gi1/0/6|||

## LACP

* SW4
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1-3
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.22.97 255.255.255.252
no shutdown
exit
interface range Gi1/0/4-6
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.22.101 255.255.255.252
no shutdown
exit
exit
wr


interface Gi1/0/7
no switchport
ip address 192.168.22.129 255.255.255.252
no sh
exit

```

* SW2
```sh
enable
configure terminal
ip routing
interface range Gi1/0/3-5
channel-group 1 mode active
exit
interface Port-channel1
no switchport
ip address 192.168.22.98 255.255.255.252
no shutdown
exit
interface range Gi1/0/1
no switchport
ip address 192.168.22.105 255.255.255.252
no shutdown
exit
interface range Gi1/0/2
no switchport
ip address 192.168.22.109 255.255.255.252
no shutdown
exit
exit
wr
```

* SW3
```sh
enable
configure terminal
ip routing
interface range Gi1/0/3-5
channel-group 2 mode active
exit
interface Port-channel2
no switchport
ip address 192.168.22.102 255.255.255.252
no shutdown
exit
interface range Gi1/0/1
no switchport
ip address 192.168.22.113 255.255.255.252
no shutdown
exit
interface range Gi1/0/2
no switchport
ip address 192.168.22.117 255.255.255.252
no shutdown
exit
exit
wr
```

* SW0
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1
no switchport
ip address 192.168.22.106 255.255.255.252
no shutdown
exit
exit
wr
```

* SW1
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1
no switchport
ip address 192.168.22.110 255.255.255.252
no shutdown
exit
interface range Gi1/0/2
no switchport
ip address 192.168.22.121 255.255.255.252
no shutdown
exit
exit
wr
```

* SW5
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1
no switchport
ip address 192.168.22.114 255.255.255.252
no shutdown
exit
interface range Gi1/0/3
no switchport
ip address 192.168.22.125 255.255.255.252
no shutdown
exit
exit
wr
```

* SW0
```sh
enable
configure terminal
ip routing
interface range Gi1/0/1
no switchport
ip address 192.168.22.118 255.255.255.252
no shutdown
exit
exit
wr
```

## EIGRP
* SW4
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.96 0.0.0.3
network 192.168.22.100 0.0.0.3
network 192.168.22.128 0.0.0.3
exit
exit
wr
```

* SW2
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.96 0.0.0.3
network 192.168.22.104 0.0.0.3
network 192.168.22.108 0.0.0.3
exit
exit
wr
```

* SW3
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.100 0.0.0.3
network 192.168.22.112 0.0.0.3
network 192.168.22.116 0.0.0.3
exit
exit
wr
```

* SW0
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.0 0.0.0.15
network 192.168.22.104 0.0.0.3
exit
exit
wr
```

* SW1
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.32 0.0.0.15
network 192.168.22.108 0.0.0.3
network 192.168.22.120 0.0.0.3
exit
exit
wr
```

* SW5
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.48 0.0.0.15
network 192.168.22.112 0.0.0.3
network 192.168.22.124 0.0.0.3
exit
exit
wr
```

* SW6
```sh
enable
configure terminal
ip routing
router eigrp 4
network 192.168.22.16 0.0.0.15
network 192.168.22.116 0.0.0.3
exit
exit
wr
```

## VLAN

|Área|Nombre|ID|
|-|-|-|
|Ventas|`VENTAS`|15|
|Facturacion|`FACTURACION`|16|

```sh
enable
configure terminal
vlan 15
name VENTAS
exit
exit
wr
```

```sh
enable
configure terminal
vlan 16
name FACTURACION
exit
exit
wr
```

### Accesos/Troncales

* SW0,SW3
```sh
enable
configure terminal
interface range Fa0/11-12
switchport access vlan 15
no shutdown
exit
interface Fa0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW1,SW2
```sh
enable
configure terminal
interface Fa0/11
switchport access vlan 15
no shutdown
exit
interface Fa0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW4,SW5

```sh
enable
configure terminal
interface Fa0/11
switchport access vlan 16
no shutdown
exit
interface Fa0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

### Interfaces VLAN
* SW0
```sh
enable
configure terminal
interface vlan 15
ip address 192.168.22.1 255.255.255.240
ip helper-address 192.168.12.38
no shutdown
exit
exit

wr
```

* SW1
```sh
enable
configure terminal
interface vlan 16
ip address 192.168.22.33 255.255.255.240
ip helper-address 192.168.12.38
no shutdown
exit
exit
wr
```

* SW5
```sh
enable
configure terminal
interface vlan 16
ip address 192.168.22.49 255.255.255.240
ip helper-address 192.168.12.38
no shutdown
exit
exit
wr
```

* SW6
```sh
enable
configure terminal
interface vlan 15
ip address 192.168.22.17 255.255.255.240
ip helper-address 192.168.12.38
no shutdown
exit
exit
wr
```