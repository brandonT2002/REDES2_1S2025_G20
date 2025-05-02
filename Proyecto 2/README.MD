<h1 align="center">Proyecto 2</h1>

<div align="center">
    <p>📕 Redes de Computadoras 2</p>
    <p>📆 Mayo 2025 | 🏛 Universidad de San Carlos de Guatemala | 👤 Grupo 20</p>
    <p><i>Modernización de Infraestructura de Red Nacional</i></p>
</div>

---

## 🛠 **Tecnologías Utilizadas**

<p align="center">
  <a href="https://go-skill-icons.vercel.app/">
    <img
      src="https://go-skill-icons.vercel.app/api/icons?i=git,github,html,css"
    />
  </a>
</p>

- **Cisco Packet Tracer** (Simulación de Red)
- **HTML y CSS3** (Página Estática)
- **GitHub** (Control de Versiones)


## 🔍 Introducción

Este manual técnico documenta la implementación de una infraestructura de red nacional para un país con una población en rápido crecimiento y una demanda de telecomunicaciones en auge. El objetivo principal es modernizar y expandir la red nacional para mejorar la conectividad, la velocidad de transmisión y la disponibilidad de servicios digitales en todas las regiones del país.

## 🧾 Descripción del Proyecto

El proyecto tiene como finalidad diseñar e implementar una infraestructura de red nacional moderna, utilizando tecnología avanzada y buenas prácticas de ingeniería de redes. Se contemplan tres proveedores de servicios de Internet (ISP), enlaces redundantes, ruteo dinámico con BGP, direccionamiento jerárquico y políticas de control de tráfico interdepartamental.

## 🗺️ Topología General

La red está conformada por 5 regiones interconectadas mediante enlaces troncales. Cada región contiene al menos un router regional que se conecta a los routers departamentales. El país contará con 3 ISPs que proveen conectividad a Internet y comunicación entre regiones.

## 📡 Direccionamiento IP

Se ha implementado un esquema de direccionamiento jerárquico para facilitar la agregación de rutas y el control del tráfico:

* Cada región tiene asignado un bloque /16.
* Cada departamento tiene un bloque /20 dentro de la región.
* Subredes internas utilizan máscaras /24 para segmentar servicios.

## 🔌 ISP: Telecom Uno

Este ISP conecta las regiones Norte y Occidente. Sus enlaces principales son de 1 Gbps y utiliza BGP con ASN 65001.

## 🔌 ISP: Redes Nacionales

Redes Nacionales interconecta las regiones Sur y Oriente, y tiene redundancia hacia la región Central. Utiliza BGP con ASN 65002.

## 🔌 ISP: Conexiones Futuras

Se contempla una futura conexión con el ISP Satelital Andino, con cobertura nacional para enlaces de respaldo vía satélite.

## 🧭 Configuración de Interconexión BGP

Cada región corre BGP para anunciar sus prefijos a los ISPs y a las demás regiones. Se utilizan políticas de route-map para:

* Filtrar rutas no deseadas.
* Priorizar rutas internas por sobre externas.
* Aplicar atributos como MED y local-pref.

### 🧮 ASN Regionales

* Región Norte: ASN 65100
* Región Sur: ASN 65101
* Región Oriente: ASN 65102
* Región Occidente: ASN 65103
* Región Central: ASN 65104

## 🛠️ Configuración de Servicios

Cada departamento implementa servicios como DNS, DHCP y servidores web locales. Se segmenta el tráfico mediante VLANs y se aplican ACLs para controlar acceso.

## 🚦 Control de Tráfico Interdepartamental

Se usan políticas de control de tráfico con:

* Rutas estáticas para tráfico crítico.
* BGP communities para clasificar tráfico.
* QoS para priorizar tráfico de voz y datos críticos.


## 📌 Conclusiones

La red nacional propuesta cumple con los objetivos de redundancia, escalabilidad y eficiencia en el manejo de tráfico. El uso de BGP entre regiones permite una administración descentralizada y resiliente. El direccionamiento jerárquico facilita futuras expansiones.

## 📚 Referencias

* RFC 4271 - Border Gateway Protocol 4 (BGP-4)
* Cisco BGP Configuration Guide
* O'Reilly - Network Warrior
* Material de clase - Redes de Computadoras 2
