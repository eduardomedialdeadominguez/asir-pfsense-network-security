# Implementación de un firewall pfSense con WAN, LAN y DMZ

## Descripción del proyecto

Práctica realizada durante el ciclo formativo de Grado Superior en Administración de Sistemas Informáticos en Red (ASIR), en el módulo de Seguridad y Alta Disponibilidad.

El objetivo es implementar un firewall pfSense en un entorno virtualizado con Oracle VirtualBox, segmentando la red en tres zonas y configurando mecanismos de control de acceso.

## Tecnologías utilizadas

- pfSense Community Edition 2.9.0
- Oracle VirtualBox
- TCP/IP
- DHCP (Dynamic Host Configuration Protocol)
- SSH (Secure Shell)
- Firewall Rules
- Network Segmentation

## Topología de red

La infraestructura se divide en tres redes:

| Interfaz | Adaptador | Dirección IP | Función |
|---|---|---|---|
| WAN | em0 | 10.0.2.15/24 (DHCP) | Acceso a Internet mediante NAT |
| LAN | em2 | 192.168.50.1/24 | Red interna de usuarios |
| DMZ | em1 | 10.0.0.1/24 | Red destinada a servidores |

## Configuraciones realizadas

### 1. Instalación y configuración de pfSense

Se instaló pfSense en una máquina virtual de VirtualBox y se asignaron tres interfaces de red independientes para WAN, LAN y DMZ.

### 2. Configuración general del firewall

Se configuraron los siguientes parámetros:

- Hostname: `MedialdeaDominguez`
- DNS principal: `8.8.8.8`
- DNS secundario: `8.8.4.4`
- DNS Override: desactivado
- Acceso al panel web mediante HTTPS

### 3. DHCP Static Mapping

Se creó una reserva DHCP para un cliente de la LAN:

- Dirección MAC: `08:00:27:72:65:E7`
- Dirección IPv4: `192.168.50.10`
- Descripción: `MedialdeaDominguezEduardo`

Esta configuración permite reservar una dirección IP para un dispositivo identificado por su dirección MAC.

### 4. Regla de filtrado SSH

Se configuró una regla de firewall con los siguientes parámetros:

| Parámetro | Valor |
|---|---|
| Acción | Pass |
| Interfaz | LAN |
| Protocolo | TCP |
| Origen | 192.168.50.10 |
| Destino | 10.0.0.50 |
| Puerto de destino | 22 (SSH) |

La regla está diseñada para permitir conexiones SSH desde el cliente de la LAN al servidor de la DMZ.

## Verificaciones

Se comprobó el acceso al panel web de administración de pfSense desde el equipo anfitrión utilizando una conexión Host-only.

También se verificó mediante la consola y la interfaz web que las tres interfaces tenían sus direcciones IPv4 configuradas.

**Pruebas pendientes:** comprobar la asignación DHCP desde el cliente especificado y realizar una conexión SSH real contra el servidor de la DMZ.

## Evidencias

Las capturas de pantalla de las configuraciones se encuentran en el directorio `screenshots/`.

## Conocimientos aplicados

- Configuración de firewalls.
- Segmentación de redes.
- Gestión de interfaces de red.
- Administración DHCP.
- Filtrado de tráfico mediante reglas.
- Control de acceso entre redes internas y DMZ.
