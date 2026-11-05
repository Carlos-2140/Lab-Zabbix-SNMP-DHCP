# Direccionamiento IP — Laboratorio Zabbix, SNMP y DHCP en GNS3

## Topología

NAT1 (red WAN de GNS3) → Router R1 → Switch SW1 → Ubuntu Server (Zabbix) y Windows 10.

## Tabla de direccionamiento

| Dispositivo | Interfaz / función | Dirección IPv4 | Máscara | Puerta de enlace / información |
|---|---|---|---|---|
| NAT1 (GNS3) | Gateway WAN | 192.168.42.1 | /24 (255.255.255.0) | Gateway recibido por R1 vía DHCP |
| Router R1 | Fa0/0 — WAN hacia NAT1 | 192.168.42.184 | /24 (255.255.255.0) | 192.168.42.1; dirección obtenida mediante DHCP |
| Router R1 | Fa0/1 — LAN hacia SW1 | 10.21.40.1 | /24 (255.255.255.0) | Gateway de la LAN |
| Switch SW1 | VLAN 1 — administración | 10.21.40.2 | /24 (255.255.255.0) | 10.21.40.1 |
| Ubuntu Server | Interfaz de red — Zabbix | 10.21.40.10 | /24 (255.255.255.0) | 10.21.40.1; reserva DHCP por identificador MAC |
| Windows 10 | Interfaz Ethernet — cliente | 10.21.40.100 | /24 (255.255.255.0) | 10.21.40.1; asignación DHCP automática |

> La dirección WAN 192.168.42.184 y la dirección Windows 10 10.21.40.100 fueron observadas durante las pruebas. Al proceder de DHCP, pueden variar si se renuevan los arrendamientos. La IP del servidor Ubuntu se reservó expresamente.

## Segmentos de red

| Segmento | Red | Máscara | Uso |
|---|---|---|---|
| WAN | 192.168.42.0/24 | 255.255.255.0 | Conexión de R1 con NAT1 |
| LAN | 10.21.40.0/24 | 255.255.255.0 | R1, SW1, Zabbix y Windows 10 |

## DHCP en Router R1

- Nombre del pool de clientes: `LAN-ZABBIX`.
- Red distribuida: `10.21.40.0/24`.
- Gateway entregado: `10.21.40.1`.
- DNS entregado: `8.8.8.8`.
- Dominio configurado: `seguridad.lab`.
- Direcciones excluidas: `10.21.40.1–10.21.40.99` y `10.21.40.151–10.21.40.254`.
- Intervalo disponible para clientes generales: `10.21.40.100–10.21.40.150`.
- Reserva independiente para Ubuntu: pool `UBUNTU-ZABBIX`, IP `10.21.40.10`, identificador de cliente `010c.4b4b.1200.00` (MAC `0c:4b:4b:12:00:00`).
- Dirección comprobada del cliente Windows 10: `10.21.40.100`.

## Equipos supervisados en Zabbix

| Host en Zabbix | IP de administración | Protocolo | Puerto | Plantilla |
|---|---|---|---|---|
| Router R1 | 10.21.40.1 | SNMPv2c | UDP 161 | Cisco IOS by SNMP |
| Switch SW1 | 10.21.40.2 | SNMPv2c | UDP 161 | Cisco IOS by SNMP |

- Servidor Zabbix: `http://10.21.40.10/zabbix` (HTTP, TCP 80).
- Los dos dispositivos se registraron en el grupo `Network devices` y su disponibilidad SNMP se verificó en verde.
- No se publica la cadena de comunidad SNMP para evitar divulgar parámetros de acceso.


