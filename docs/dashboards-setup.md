# Dashboards Setup - OpenSOC Network Defense

## 📊 Objetivo
Diseñar y configurar dashboards personalizados en Kibana para la monitorización efectiva de alertas, eventos y análisis de tráfico de red.

---

## 🔹 Componentes Monitorizados
- Suricata (IDS/IPS)
- Wazuh (Host-based Intrusion Detection)
- Zeek (Network Analysis)
- Filebeat (Log Collector)

---

## 🔧 Procedimiento de Configuración

### 1. Configuración de Index Patterns
En Kibana, crear los siguientes index patterns:
- `filebeat-*`
- `wazuh-alerts-*`
- `zeek-*` (si Zeek está integrado opcionalmente)

### 2. Dashboards principales creados

#### 🔒 Security Overview
- Top 10 IPs origen con más alertas.
- Alertas por tipo de ataque (Brute Force, SQLi, Port Scanning).
- Alertas por severidad.

#### 📱 Endpoint Monitoring (Wazuh)
- Eventos de integridad de archivos.
- Cambios sospechosos en configuración.
- Accesos fallidos.

#### 🔎 Network Threat Detection (Suricata)
- Detección de escaneos de puertos.
- Análisis de ataques HTTP.
- Estadísticas de protocolos detectados.

#### 🌐 Passive Traffic Analysis (Zeek & TShark)
- Sesiones TCP anómalas.
- Análisis de certificados TLS sospechosos.
- Estadísticas de dominios DNS consultados.

### 3. Visualizaciones utilizadas
- Data Tables
- Pie Charts
- Line Graphs
- Heatmaps

### 4. Creación de Alertas en Kibana (Opcional)
Reglas configuradas para:
- Múltiples intentos de acceso fallidos.
- Escaneos de red sospechosos.
- Posible SQL Injection detectado.

---

## 🔄 Actualización Continua
Los dashboards son revisados y ajustados periódicamente en función de:
- Nuevas reglas en Suricata.
- Actualización de reglas en Wazuh.
- Análisis de nuevos escenarios de ataque.