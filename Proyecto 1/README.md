## Asignación de IPs

|Vlan|Subred|Rango|Broadcast|Máscara de Subred|
|-|-|-|-|-|
|VLAN_Verde_EdificioIZQ_20|192.168.20.0/27|192.168.20.1 - 192.168.20.30|192.168.20.31|255.255.255.224|
|VLAN_Naranja_EdificioIZQ_20|192.168.20.32/27|192.168.20.33 - 192.168.20.62|192.168.20.63|255.255.255.224|
|VLAN_Verde_EdificioDER_20|192.168.20.64/27|192.168.20.65 - 192.168.20.94|192.168.20.95|255.255.255.224|
|VLAN_Naranje_EdificioDER_20|192.168.20.96/27|192.168.20.97 - 192.168.20.126|192.168.20.127|255.255.255.224|
|VLAN_Admin_20|192.168.20.128/27|192.168.20.129 - 192.168.20.158|192.168.20.1259|255.255.255.224|

|#|Subred|Rango|Broadcast|Máscara de Subred|
|-|-|-|-|-|
|1|10.0.20.0/27|10.0.20.1 - 10.0.20.30|10.0.20.31|255.255.255.224|
|2|10.0.20.32/27|10.0.20.33 - 10.0.20.62|10.0.20.63|255.255.255.224|
|3|10.0.20.64/27|10.0.20.65 - 10.0.20.94|10.0.20.95|255.255.255.224|
|4|10.0.20.96/27|10.0.20.97 - 10.0.20.126|10.0.20.127|255.255.255.224|
|5|10.0.20.128/27|10.0.20.129 - 10.0.20.158|10.0.20.159|255.255.255.224|
|6|10.0.20.160/27|10.0.20.161 - 10.0.20.190|10.0.20.191|255.255.255.224|
|7|10.0.20.192/27|10.0.20.193 - 10.0.20.222|10.0.20.223|255.255.255.224|

## Modos Troncales

* SW4
```sh
enable
configure terminal
interface range f0/1-6
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* SW5, SW6
```sh
enable
configure terminal
interface range f0/1-4
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

* S2, S3
```sh
enable
configure terminal
interface f0/1
switchport mode trunk
switchport trunk allowed vlan all
exit
exit
wr
```

## Modo Cliente
* S2 - S3, SW5 - SW6
```sh
enable
configure terminal
vtp mode client
vtp domain g20
vtp password usac
exit
wr
show vtp status
```

#### Modo Servidor
* SW4
```sh
enable
configure terminal
vtp mode server
vtp domain g20
vtp password usac
vtp version 2
exit
wr
show vtp status
```

#### Modo Acceso
* S2
```sh
enable
configure terminal
interface range fa0/10-11
switchport mode access
switchport Access vlan 6
exit
exit
wr
show interface status
```

* S3
```sh
enable
configure terminal
interface range fa0/10-11
switchport mode access
switchport Access vlan 5
exit
exit
wr
show interface status
```

### VLAN
```sh
enable
configure terminal
vlan 5
name VLAN_Naranja_EdificioDER_20
exit
vlan 6
name VLAN_Verde_EdificioDER_20
exit
exit
wr
show vlan
```