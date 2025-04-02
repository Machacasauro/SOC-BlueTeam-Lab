# Proyecto Completo: Implementación de un SOC con Suricata, Wazuh, ELK Stack y Simulación de Incidentes

## Objetivo
Desarrollar un entorno funcional de detección y respuesta a incidentes utilizando herramientas open-source para simular un entorno real de un SOC (Security Operations Center).

## Descripción
Blue Team Lab es un proyecto personal y profesional donde he diseñado, implementado y gestionado un entorno completo de detección y respuesta ante amenazas, basado en tecnologías Open Source. Todos los sistemas han sido instalados, configurados y personalizados manualmente, sin el uso de distribuciones preconfiguradas.

Este laboratorio tiene como objetivo demostrar mis capacidades técnicas en la administración de infraestructuras de ciberseguridad, análisis de incidentes y respuesta a amenazas en entornos empresariales.

## Certificaciones y formación relevantes
- Cisco Cybersecurity Operations Fundamentals  (200-201 CBROPS)
- TryHackMe SOC Level 1
- Mikrotik (MTCNA, MTCRE, MTCWE) Reglas de firewall perimetral, Qos, 

## 📚 Índice del Proyecto

1. Arquitectura del Proyecto
2. Implementación Técnica
3. Simulación de Escenarios de Ataques
4. Análisis y Correlación de Eventos
5. Automatización y Gestión de Vulnerabilidades
6. Inteligencia de Amenazas (CTI/OSINT)
7. Análisis Forense Digital (DFIR)
8. Documentación Técnica y Playbooks
9. Certificaciones Complementarias y Futuras

---

## 1. Arquitectura del Proyecto

**Entorno:**
- SO: Ubuntu Server 22.04 LTS (Servidor Apache, Mysql, Documental) Lab
- IDS/IPS: Suricata
- SIEM: ELK Stack (Elasticsearch, Logstash, Kibana)
- EDR: Wazuh
- Herramientas adicionales Kali Linux: Hydra, Nmap, TryHackMe labs, Zeek, TShark
- DFIR: REMnux v7

**Diagrama de Arquitectura:**

- Suricata: Monitorea el tráfico de red en modo IDS, generando alertas.
- Filebeat: Recolecta logs de Suricata y los envía a Logstash.
- Logstash: Parseo y enriquecimiento de los logs.
- Elasticsearch: Almacenamiento de los eventos.
- Kibana: Visualización y análisis de los datos.
- Wazuh: Correlación de eventos, integración con Filebeat y Active-Response.
- Zeek y TShark: Análisis pasivo y forense de tráfico de red.

---

## 2. Implementación Técnica

### Instalación y configuración de Elastic Stack

- Elasticsearch, Logstash y Kibana instalados desde repositorios oficiales.
- Configuración personalizada de pipelines y dashboards.

### Instalación y configuración de Suricata

```bash
sudo apt-get update
sudo apt-get install suricata -y
sudo suricata -i eth0 -c /etc/suricata/suricata.yaml --af-packet
```

**Configuración en suricata.yaml:**

```
outputs:
  eve-log:
    enabled: yes
    filetype: regular
    filename: /var/log/suricata/eve.json
    types:
      - alert
      - http
      - dns
      - tls
      - flow
```

**Reglas personalizadas:**

```bash
sudo nano /etc/suricata/rules/custom.rules
```

Ejemplos:
- Detección de SSH Brute Force
- HTTP GET Flood
- MySQL Brute Force
- ICMP DoS Attack
- Jumbo Frames

Verificación:
```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

### Instalación y configuración de Filebeat

```bash
sudo apt-get install filebeat
sudo filebeat modules enable suricata
sudo nano /etc/filebeat/filebeat.yml
```

Configuración:
```yaml
output.logstash:
  hosts: ["localhost:5044"]
```

Inicio:
```bash
sudo systemctl start filebeat
sudo systemctl enable filebeat
```

### Integración y verificación

- Confirmar que los logs fluyen correctamente.
- Revisar dashboards en Kibana.

### Instalación de Zeek (independiente)

```bash
sudo apt-get install zeek -y
sudo zeekctl deploy
```

Zeek opera como sistema independiente para análisis pasivo.

---

## 3. Simulación de Escenarios de Ataques

- SSH Brute Force con Hydra:
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://tu-ip-servidor
```

- Escaneo de puertos con Nmap:
```bash
nmap -sS -p 1-65535 tu-ip-servidor
```

- SQL Injection:
```bash
sqlmap -u "http://target.com/vuln.php?id=1" --risk=3 --level=5 --batch
```

---

## 4. Análisis y Correlación de Eventos

- Revisar alertas de Suricata en Kibana.
- Correlación mediante Wazuh.
- Uso de TShark y Zeek para análisis pasivo.

---

## 5. Automatización y Gestión de Vulnerabilidades

- Automatización de despliegue de reglas.
- Generación de reportes semanales.
- Uso de OpenVAS para escaneo de vulnerabilidades.

---

## 6. Inteligencia de Amenazas (CTI/OSINT)

- Integración de fuentes OSINT:
  - AbuseIPDB

---

## 7. Análisis Forense Digital (DFIR)

- Extracción y análisis de logs post-incidente.
- Uso de Wireshark, Zeek y Volatility para investigación avanzada.

---

## 8. Documentación Técnica y Playbooks

- Procedimientos detallados para:
  - Instalación de cada componente.
  - Respuesta ante incidentes.
  - Análisis forense.

---

## 9. Certificaciones Complementarias y Futuras

- Próxima certificaciuón: Security Analyst Level 1 (SAL1)
- Preparación activa para: eJPT v2 (INE Security)


---

## 📅 Troubleshooting y Problemas Solventados

- Configuración errónea en suricata.yaml: Se solucionó verificando la sintaxis y usando `suricata -T`.
- Problemas de conexión entre Filebeat y Logstash: Ajuste de puertos y configuración YAML.
- Wazuh agent no enviaba logs: Se resolvió ajustando las claves y verificando la conectividad.
- Error de parsing en Logstash: Revisión y corrección de grok patterns.
- Fallos en la integración Kibana-Wazuh: Instalación de plugin correcto y ajuste de roles.