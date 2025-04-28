
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

router eigrp 1       
network 192.168.12.0 0.0.0.7   
network 192.168.12.8 0.0.0.7  
network 192.168.12.16 0.0.0.7   
network 192.168.12.24 0.0.0.7  
network 192.168.12.32 0.0.0.31 
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
network 192.168.12.32 0.0.0.31  
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



