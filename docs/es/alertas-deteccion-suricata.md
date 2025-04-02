
# 🛡️ Reglas de Detección Suricata - Alertas Capturadas

Este documento contiene las alertas generadas por Suricata y visualizadas en Kibana como parte del proyecto SOC Blue Team Lab. Cada alerta representa un escenario de amenaza diferente, simulado y analizado dentro del laboratorio.



## 🚀 1. HTTP GET Flood Detectado

![HTTP GET Flood Detectado](../../images/HTTPSGETFloodDetected.jpg)

**Descripción:**  
Se detectó un volumen elevado de peticiones HTTP GET, indicativo de un intento de Denegación de Servicio (DoS) mediante un ataque conocido como HTTP GET Flood.



## 🔒 2. Conexiones HTTPS Sospechosas

![Conexiones HTTPS Sospechosas](../../images/HTTPSSuspiciousConnections.jpg)

**Descripción:**  
Se identificaron múltiples conexiones TLS/HTTPS marcadas como sospechosas. Este comportamiento puede estar relacionado con actividades de reconocimiento o escaneo automatizado de servicios HTTPS.



## 🌐 3. ICMP DoS Attack Detectado

![ICMP DoS Attack Detectado](../../images/ICMPDoSAttackDetected.jpg)

**Descripción:**  
Se detectó un flujo elevado de tráfico ICMP. Este comportamiento es típico de un ataque de Denegación de Servicio (DoS) utilizando paquetes ICMP Echo Request.



## 🔍 4. Nmap ACK Scan Detectado

![Nmap ACK Scan Detectado](../../images/NMAPAckScanDetected.jpg)

**Descripción:**  
Suricata identificó un escaneo de red consistente con un escaneo ACK de Nmap. Este tipo de escaneo se utiliza para mapear reglas de firewall y descubrir puertos no filtrados.



## ⚠️ 5. Posible Ataque XSS Detectado

![Posible Ataque XSS Detectado](../../images/PossibleXSSAttackDetected.jpg)

**Descripción:**  
Se detectó un posible intento de ataque Cross-Site Scripting (XSS), en el que se intentó inyectar código malicioso en peticiones HTTP para manipular scripts del lado del cliente.



## 🧩 6. Escaneo de Puertos de Servicios Detectado

![Escaneo de Puertos de Servicios Detectado](../../images/ServicesPortsScanDetected.jpg)

**Descripción:**  
Se identificó actividad de escaneo de puertos dirigida a servicios conocidos (SSH, HTTP, HTTPS, MySQL). Este comportamiento es comúnmente asociado a tareas de reconocimiento.



## 🔑 7. Ataque de Fuerza Bruta SSH Detectado

![Ataque de Fuerza Bruta SSH Detectado](../../images/SSHBruteForceDetected.jpg)

**Descripción:**  
Suricata detectó múltiples intentos de acceso no autorizado al servicio SSH mediante técnicas de fuerza bruta.



## 📄 Resumen

Todos estos eventos fueron generados en un entorno controlado como parte de los ejercicios de detección, análisis y defensa Blue Team utilizando Suricata, ELK Stack y Wazuh.

