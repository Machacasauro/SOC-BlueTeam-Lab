# Attack Simulation - OpenSOC Network Defense

## 🔎 Objetivo
Simular escenarios de ataque en un entorno controlado para validar la eficacia de las soluciones de detección y respuesta implementadas en el proyecto OpenSOC Network Defense.



## 🔫 Escenarios de Ataques Simulados

### 1. SSH Brute Force Attack
- **Herramienta:** Hydra
- **Comando ejecutado:**
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.10.5
```
- **Resultado esperado:**
  - Alerta en Suricata y Wazuh.
  - Evento correlacionado en Kibana.
  - Bloqueo automático de IP en Wazuh Active-Response.



### 2. Escaneo de Puertos con Nmap
- **Herramienta:** Nmap
- **Comando ejecutado:**
```bash
nmap -sS -p 1-65535 192.168.10.5
```
- **Resultado esperado:**
  - Detección del escaneo SYN por Suricata.
  - Registro del evento en Wazuh y visualización en Kibana.
  - Logs detallados en Zeek.



### 3. SQL Injection
- **Herramienta:** SQLMap
- **Comando ejecutado:**
```bash
sqlmap -u "http://192.168.10.5/vuln.php?id=1" --risk=3 --level=5 --batch
```
- **Resultado esperado:**
  - Detección por Suricata mediante reglas HTTP.
  - Evento registrado en Wazuh.
  - Análisis complementario en TShark y Zeek.



### 4. ICMP DoS Attack
- **Herramienta:** hping3
- **Comando ejecutado:**
```bash
hping3 -1 --flood -V 192.168.10.5
```
- **Resultado esperado:**
  - Detección por Suricata y Wazuh.
  - Evento visualizado en Kibana.



## 🔎 Análisis Complementario
- **TShark:** Utilizado para capturar y analizar paquetes durante los ataques.
- **Zeek:** Generación de logs de actividad de red para análisis detallado.



## 📅 Validación de Detección
Cada ataque simulado ha sido validado verificando:
- La generación correcta de alertas en Suricata y Wazuh.
- La correlación de eventos en Kibana.
- La captura de tráfico en Zeek y TShark.
- La aplicación de respuesta automática (cuando corresponde).