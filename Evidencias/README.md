# Evidencias del laboratorio GNS3 — Zabbix, SNMP y DHCP

Esta carpeta reúne capturas **reales** de la práctica. No deben sustituirse por ilustraciones ni capturas simuladas.

## Organización recomendada

- `01-Topologia/`: vista general de NAT1, R1, SW1, Ubuntu y Windows 10.
- `02-DHCP/`: configuración del pool, reserva de Ubuntu y tabla de asignaciones.
- `03-Ubuntu/`: dirección IP del servidor Zabbix obtenida por DHCP.
- `04-Zabbix/`: hosts, parámetros SNMP, datos recopilados, gráficas, dashboard y alertas.
- `05-Pruebas-Adicionales/`: conectividad, NAT y SNMP en consola **solo si se dispone de capturas reales**.

## Direcciones verificadas

| Dispositivo | IP |
|---|---|
| R1 LAN | 10.21.40.1/24 |
| SW1 administración | 10.21.40.2/24 |
| Ubuntu Zabbix | 10.21.40.10/24 |
| Windows 10 | 10.21.40.100/24 |

## Relación de evidencias

| Archivo | Descripción |
|---|---|
| `01-Topologia/01-Topologia-GNS3.png` | Diagrama real de conexiones GNS3 |
| `02-DHCP/02-R1-Configuracion-DHCP.png` | Exclusiones, pool LAN-ZABBIX y reserva UBUNTU-ZABBIX |
| `02-DHCP/03-R1-DHCP-BINDINGS.png` | Asignaciones manual y automática |
| `03-Ubuntu/04-Ubuntu-IP.png` | Dirección 10.21.40.10/24 en ens3 |
| `04-Zabbix/` | Capturas originales del informe de Zabbix |

Las imágenes de Zabbix muestran información de monitoreo, configuración SNMPv2, estado de hosts y alertas. **Antes de publicar** capturas de parámetros SNMP, se debe ocultar la cadena de comunidad para no divulgar credenciales de acceso.

Las advertencias half-duplex que muestra Zabbix se conservan como hallazgos reales; no se presentan como incidencias resueltas.

> Nota: este índice documenta la organización prevista. Los archivos PNG deben cargarse por separado al repositorio para que aparezcan en GitHub.
