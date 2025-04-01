# SOC-BlueTeam-Lab
OpenSOC Network Defense Lab — Blue Team Architecture &amp; Threat Detection
Repositorio: OpenSOC-Network-Defense-Lab

🎯 Descripción
OpenSOC Network Defense Lab es un proyecto personal y profesional donde he diseñado, implementado y gestionado un entorno completo de detección y respuesta ante amenazas, basado en tecnologías Open Source. Todos los sistemas han sido instalados, configurados y personalizados manualmente desde cero, sin el uso de distribuciones preconfiguradas.

Este laboratorio tiene como objetivo demostrar mis capacidades técnicas en la administración de infraestructuras de ciberseguridad, análisis de incidentes y respuesta a amenazas en entornos empresariales.

🗂️ Índice del Proyecto
Arquitectura del Proyecto

1. Implementación Técnica

2. Integración y Correlación de Eventos

3. Escenarios de Ataque Simulados

4. Análisis Forense y Gestión de Vulnerabilidades

5. Inteligencia de Amenazas (CTI/OSINT)

6. Documentación Técnica y Playbooks

7. Certificaciones y Formación Relevantes

🏗️ Arquitectura del Proyecto

+----------------------+        +-----------------------+
|  Attacker (Kali)     | -----> | Suricata + Zeek IDS  |
+----------------------+        +-----------------------+
                                      |
                                      v
+----------------------+        +-----------------------+
| Wazuh Server        |<------->| Elastic Stack (ELK)  |
+----------------------+        +-----------------------+
                                      |
                                      v
+----------------------+        +-----------------------+
| Kibana Dashboard    |<------->| Analyst Workstation  |
+----------------------+        +-----------------------+

⚙️ Implementación Técnica

* Instalación manual de Elasticsearch, Logstash y Kibana en Ubuntu Server.

Configuración personalizada de Wazuh desde repositorios oficiales.

Instalación y tuning de Suricata IDS con reglas personalizadas.

Integración de logs de Suricata mediante Filebeat.

Instalación de Zeek en modo independiente para análisis pasivo.

Configuración de dashboards personalizados en Kibana para correlación de eventos.

🔥 Simulación de Escenarios de Ataques
Escenario	Herramienta	Detección
SSH Brute Force	Hydra	Wazuh + Kibana
Nmap Scan	Nmap	Suricata + Zeek
SQL Injection	SQLMap	Suricata + Wazuh
🔐 Análisis, Correlación y Respuesta
Detección y bloqueo automático de IPs maliciosas mediante Active-Response.

Correlación de alertas y visualización unificada en Kibana.

Playbooks documentados para análisis y respuesta a incidentes.

📊 Inteligencia de Amenazas (CTI/OSINT)
Enriquecimiento de alertas con fuentes OSINT.

Incorporación de indicadores de compromiso (IOCs) de fuentes públicas.

🧩 Documentación y Playbooks
Disponible en la carpeta /Documentation:

Guía de instalación paso a paso.

Manual de operación.

Procedimientos de respuesta ante incidentes.

🎓 Certificaciones y Formación
CBROPS 200-201 (Cisco CyberOps Associate)

TryHackMe SOC Level 1

Formación práctica continua en TryHackMe y preparación para el certificado eJPT v2.
