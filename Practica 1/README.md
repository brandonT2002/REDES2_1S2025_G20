<h1 align="center">Practica 1</h1>
<div align="center">
👨‍👨‍👦 Grupo 20
</div>
<div align="center">
📕 Redes de Computadoras 2
</div>
<div align="center"> 🏛 Universidad San Carlos de Guatemala</div>
<div align="center"> 📆 Primer Semestre 2025</div>


# **📘 Manual Técnico**  

## **1️⃣ Introducción**  
### **🎯 1.1 Objetivo del documento**  
Este documento describe la implementación y configuración de la red en **Cisco Packet Tracer**, siguiendo los requerimientos establecidos en la práctica. Se detallan las configuraciones de **VLANs, VTP, STP, seguridad en puertos, enrutamiento dinámico**, y otros aspectos esenciales.  

### **🌍 1.2 Descripción del escenario**  
El colegio **Alma Mater** necesita optimizar su red, ya que ha perdido el control sobre las configuraciones previas. Se requiere la implementación de medidas para mejorar la **segmentación, seguridad y rendimiento** de la red.  

## **2️⃣ Topología de Red**  
### **🖥️ 2.1 Diagrama de Red**  
_(Adjuntar imagen con la topología diseñada en Packet Tracer, incluyendo nombres de dispositivos, conexiones y VLANs.)_  

### **📌 2.2 Equipos utilizados**  
| Dispositivo | Modelo | Cantidad |  
|------------|--------|----------|  
| Switch Layer 2 | Cisco [2960-24TT] | 22 |  
| Router | Cisco [2901] | 4 |  
| PC | PC-PT | 8 |  
| Laptop | Laptop-PT | 2 |

### **🌐 2.3 Direccionamiento IP**  

- Calculo de VLAN

  - **Lado Derecho**
  - Primaria = 10 + #Grupo
  - Basicos = 20 + #Grupo
  - Diversificado = 30 + #Grupo

  - **Lado Izquierdo**
  - Primaria = 40 + #Grupo
  - Basicos = 50 + #Grupo
  - Diversificado = 60 + #Grupo

- Numero de Grupo: **20**

  - **Lado Derecho**
  - Primaria → *10 + (20) → 10 + (2+0)* = **12**
  - Basicos → *20 + (20) → 20 + (2+0)* = **22**
  - Diversificado → *30 + (20) → 30 + (2+0)* = **32**

  - **Lado Izquierdo**
  - Primaria → *40 + (20) → 40 + (2+0)* = **42**
  - Basicos → *50 + (20) → 50 + (2+0)* = **52**
  - Diversificado → *60 + (20) → 60 + (2+0)* = **62**

Cada subred tiene un esquema de direccionamiento basado en VLANs:  

| VLAN | Nombre | Dirección de Red | Máscara | Gateway |  
|------|--------|-----------------|---------|---------|  
| 12 | Primaria (izq) | 192.168.12.0/24 | 255.255.255.0 | 192.168.12.1 |  
| 22 | Básicos (izq) | 192.168.22.0/24 | 255.255.255.0 | 192.168.22.1 |  
| 32 | Diversificado (izq) | 192.168.32.0/24 | 255.255.255.0 | 192.168.32.1 |  
| 42 | Primaria (der) | 192.168.42.0/24 | 255.255.255.0 | 192.168.42.1 |  
| 52 | Básicos (der) | 192.168.52.0/24 | 255.255.255.0 | 192.168.52.1 |  
| 62 | Diversificado (der) | 192.168.62.0/24 | 255.255.255.0 | 192.168.62.1 |  

### **🌐 2.4 Configuración dirección de red PC's**


| Dispositivo | Direccion IP | Mascara de Red | VLAN | Default Gateway |
| ----------- | ------------ | -------------- | -------------- | --------------- |
| PC1 | 192.168.12.X | 255.255.255.0 | 17 | 192.168.12.1 |
| PC2 | 192.168.12.X | 255.255.255.0 | 17 | 192.168.12.1 |
| PC3 | 192.168.52.X | 255.255.255.0 | 17 | 192.168.52.1 |
| PC4 | 192.168.32.X | 255.255.255.0 | 27 | 192.168.32.1 |
| PC5 | 192.168.32.X | 255.255.255.0 | 17 | 192.168.32.1 |
| PC6 | 192.168.42.X | 255.255.255.0 | 17 | 192.168.42.1 |
| PC7 | 192.168.42.X | 255.255.255.0 | 17 | 192.168.42.1 |
| PC8 | 192.168.52.X | 255.255.255.0 | 17 | 192.168.52.1 |
| LAPTOP1 | 192.168.22.X | 255.255.255.0 | 37 | 192.168.22.1 |
| LAPTOP2 | 192.168.62.X | 255.255.255.0 | 37 | 192.168.62.1 |

## **3️⃣ Configuración de Dispositivos**  
### **🔧 3.1 Configuración de Switches**  
#### **📝 3.1.1 Cambio de nombre y contraseñas**  
```plaintext  
Switch> enable  
Switch# configure terminal  
Switch(config)# hostname SW1_G20  
Switch(config)# enable secret redes2grupo#B  
```  

#### **🔀 3.1.2 Configuración de VLANs**  
```plaintext  
Switch(config)# vlan 12  
Switch(config-vlan)# name Primaria10  
Switch(config)# vlan 22 
Switch(config-vlan)# name Basicos20  
...  
```  

#### **📡 3.1.3 Configuración de VTP**  
```plaintext  
Switch(config)# vtp domain g20  
Switch(config)# vtp mode server  
Switch(config)# vtp password secureVTP  
```  

#### **🔌 3.1.4 Configuración de Trunking**  
```plaintext  
Switch(config)# interface fa0/1  
Switch(config-if)# switchport mode trunk  
Switch(config-if)# switchport trunk allowed vlan 12,22,32,42,52,62  
```  

#### **🔐 3.1.5 Configuración de Port Security**  
```plaintext  
Switch(config)# interface fa0/10  
Switch(config-if)# switchport mode access  
Switch(config-if)# switchport port-security  
Switch(config-if)# switchport port-security mac-address sticky  
Switch(config-if)# switchport port-security maximum 1  
Switch(config-if)# switchport port-security violation shutdown  
```  

### **🔄 3.2 Configuración de STP (Spanning Tree Protocol)**  
#### **🌳 3.2.1 Configuración de PVST**  
```plaintext  
Switch(config)# spanning-tree mode pvst  
Switch(config)# spanning-tree vlan 12 priority 24576  
```  

#### **⚡ 3.2.2 Configuración de Rapid PVST**  
```plaintext  
Switch(config)# spanning-tree mode rapid-pvst  
Switch(config)# spanning-tree vlan 42 priority 24576  
```  

### **🚦 3.3 Configuración de Enrutamiento Dinámico**  

#### 📡 Router 0

```
interface GigabitEthernet0/0
 ip address 10.0.21.1 255.255.255.0
 no shutdown
 exit

interface GigabitEthernet0/1
 no ip address
 no shutdown
 exit

interface GigabitEthernet0/1.12
 encapsulation dot1Q 12
 ip address 192.168.12.1 255.255.255.0
 exit

interface GigabitEthernet0/1.22
 encapsulation dot1Q 22
 ip address 192.168.22.1 255.255.255.0
 exit

interface GigabitEthernet0/1.32
 encapsulation dot1Q 32
 ip address 192.168.32.1 255.255.255.0
 exit

router ospf 50
 log-adjacency-changes
 redistribute rip metric 10 subnets
 network 10.0.21.0 0.0.0.255 area 0
 network 192.168.12.0 0.0.0.255 area 0
 network 192.168.22.0 0.0.0.255 area 0
 network 192.168.32.0 0.0.0.255 area 0
 exit

router rip
 version 2
 network 10.0.0.0
 exit

write memory
```

#### 📡 Router1

```
enable
configure terminal

interface GigabitEthernet0/0
 ip address 10.0.21.2 255.255.255.0
 no shutdown
 duplex auto
 speed auto
 exit

interface GigabitEthernet0/1
 ip address 10.0.22.1 255.255.255.0
 no shutdown
 duplex auto
 speed auto
 exit

router ospf 50
 log-adjacency-changes
 network 10.0.21.0 0.0.0.255 area 0
 distance 125
 exit

router rip
 version 2
 redistribute ospf 50 metric 2
 network 10.0.0.0
 no auto-summary
 exit

write memory
```


#### 📡 Router 2

```
enable
configure terminal

interface GigabitEthernet0/0
 ip address 10.0.23.1 255.255.255.0
 no shutdown
 duplex auto
 speed auto
 exit

interface GigabitEthernet0/1
 ip address 10.0.22.2 255.255.255.0
 no shutdown
 duplex auto
 speed auto
 exit

router eigrp 10
 network 10.0.23.0 0.0.0.255
 exit

router rip
 version 2
 redistribute eigrp 10 metric 5
 network 10.0.0.0
 no auto-summary
 exit

write memory
```


#### 📡 Router 3

```
enable
configure terminal

interface GigabitEthernet0/0
 ip address 10.0.23.2 255.255.255.0
 no shutdown
 duplex auto
 speed auto
 exit

interface GigabitEthernet0/1
 no ip address
 no shutdown
 duplex auto
 speed auto
 exit

interface GigabitEthernet0/1.42
 encapsulation dot1Q 42
 ip address 192.168.42.1 255.255.255.0
 no shutdown
 exit

interface GigabitEthernet0/1.52
 encapsulation dot1Q 52
 ip address 192.168.52.1 255.255.255.0
 no shutdown
 exit

interface GigabitEthernet0/1.62
 encapsulation dot1Q 62
 ip address 192.168.62.1 255.255.255.0
 no shutdown
 exit

router eigrp 10
 redistribute rip metric 2560 0 255 255 1500
 network 10.0.23.0 0.0.0.255
 network 192.168.42.0
 network 192.168.52.0
 network 192.168.62.0
 exit

router rip
 version 2
 network 10.0.0.0
 no auto-summary
 exit

write memory
```

## **4️⃣ Pruebas y Validación**  
### **🖧 4.1 Verificación de Conectividad**  
Ejecutar `ping` entre hosts en distintas VLANs y entre edificios.  

### **🔎 4.2 Verificación de STP y Convergencia**  
Medir tiempos de convergencia eliminando enlaces y usando:  
```plaintext  
Switch# show spanning-tree  
```  

### **📡 4.3 Verificación de Enrutamiento**  
Comprobar las rutas con:  
```plaintext  
Router# show ip route  
```  

## **5️⃣ Resultados**  
| Escenario | Protocolo Spanning-Tree | Red Primaria | Red Básicos | Red Diversificado |  
|---|---|---|---|---|  
| 1 | PVST |  |  |  |  
| 2 | Rapid PVST |  |  |  |  