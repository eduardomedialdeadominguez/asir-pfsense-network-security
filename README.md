# Configuración de un firewall pfSense en VirtualBox

## Descripción

En este proyecto he instalado y configurado un firewall pfSense utilizando VirtualBox como entorno de virtualización.

Esta práctica la he realizado en el módulo de **Seguridad y Alta Disponibilidad** del Grado Superior de Administración de Sistemas Informáticos en Red (ASIR).

El objetivo ha sido aprender a configurar un firewall, dividir una red en diferentes zonas y controlar las comunicaciones entre ellas.

## Herramientas utilizadas

- pfSense CE 2.9.0
- Oracle VirtualBox
- TCP/IP
- DHCP
- SSH
- Firewall Rules

## Esquema de red

Para realizar la práctica he utilizado tres interfaces de red:

| Interfaz | Dirección IP | Función |
|---|---|---|
| WAN (em0) | 10.0.2.15/24 | Conexión a Internet mediante NAT |
| LAN (em2) | 192.168.50.1/24 | Red interna |
| DMZ (em1) | 10.0.0.1/24 | Red destinada a servidores |

He separado la LAN y la DMZ para poder controlar el tráfico entre ambas mediante pfSense.

## Configuración realizada

### 1. Instalación de pfSense

Primero he creado una máquina virtual en VirtualBox y he instalado pfSense CE 2.9.0.

Después he configurado tres adaptadores de red para separar la conexión a Internet, la red LAN y la DMZ.

Una vez instalado, he asignado las interfaces y configurado sus direcciones IP.

### 2. Configuración general

He accedido al panel de administración web de pfSense desde mi ordenador utilizando una conexión Host-only.

Dentro del apartado **General Setup**, he configurado:

- Hostname: `MedialdeaDominguez`
- DNS principal: `8.8.8.8`
- DNS secundario: `8.8.4.4`
- DNS Override: desactivado

También he mantenido HTTPS para acceder al panel de administración de forma cifrada.

### 3. Reserva de dirección IP mediante DHCP

He creado un **DHCP Static Mapping** para reservar una dirección IP a un cliente de la LAN.

Los datos utilizados han sido:

- MAC: `08:00:27:72:65:E7`
- IP: `192.168.50.10`
- Descripción: `MedialdeaDominguezEduardo`

De esta forma, cuando un dispositivo con esa dirección MAC solicite una IP al servidor DHCP, podrá recibir la dirección que he reservado.

### 4. Configuración de una regla de firewall para SSH

Por último, he creado una regla en la interfaz LAN para permitir conexiones SSH hacia un servidor situado en la DMZ.

He utilizado los siguientes parámetros:

| Parámetro | Configuración |
|---|---|
| Action | Pass |
| Interface | LAN |
| Protocol | TCP |
| Source | 192.168.50.10 |
| Destination | 10.0.0.50 |
| Destination Port | SSH (22) |

Con esta regla he definido qué equipo puede iniciar conexiones SSH hacia el servidor de la DMZ.

## Comprobaciones realizadas

Durante la práctica he comprobado que podía acceder al panel web de pfSense desde mi ordenador y que las tres interfaces estaban configuradas con las direcciones IP correspondientes.

También he revisado la reserva DHCP y la regla de filtrado creada.

Me queda pendiente comprobar la conexión SSH real con el servidor Ubuntu de la DMZ y verificar que el cliente recibe la IP reservada mediante DHCP.

## Capturas de pantalla

En la carpeta `screenshots` he organizado las capturas de las configuraciones realizadas durante la práctica.

## Qué he aprendido

Con esta práctica he podido trabajar con un firewall real en un entorno virtualizado y entender mejor cómo se separan las redes utilizando WAN, LAN y DMZ.

También he practicado la asignación de direcciones IP, las reservas DHCP y la creación de reglas para controlar qué equipos pueden comunicarse entre diferentes redes.
