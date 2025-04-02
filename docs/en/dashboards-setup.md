# Dashboards Setup - OpenSOC Network Defense

## 📊 Objective
Design and configure customized dashboards in Kibana for effective monitoring of alerts, events, and network traffic analysis.

---

## 🔹 Monitored Components
- Suricata (IDS/IPS)
- Wazuh (Host-based Intrusion Detection)
- Zeek (Network Analysis)
- Filebeat (Log Collector)

---

## 🔧 Configuration Procedure

### 1. Index Patterns Configuration
In Kibana, create the following index patterns:
- `filebeat-*`
- `wazuh-alerts-*`
- `zeek-*` (if Zeek is optionally integrated)

### 2. Main Dashboards Created

#### 🔒 Security Overview
- Top 10 source IPs with most alerts.
- Alerts by attack type (Brute Force, SQLi, Port Scanning).
- Alerts by severity.

#### 📱 Endpoint Monitoring (Wazuh)
- File integrity events.
- Suspicious configuration changes.
- Failed access attempts.

#### 🔎 Network Threat Detection (Suricata)
- Port scan detection.
- HTTP attack analysis.
- Detected protocols statistics.

#### 🌐 Passive Traffic Analysis (Zeek & TShark)
- Anomalous TCP sessions.
- Analysis of suspicious TLS certificates.
- DNS domain query statistics.

### 3. Visualizations Used
- Data Tables
- Pie Charts
- Line Graphs
- Heatmaps

### 4. Kibana Alerts Configuration (Optional)
Rules configured for:
- Multiple failed access attempts.
- Suspicious network scans.
- Possible SQL Injection detected.

---

## 🔄 Continuous Updates
Dashboards are periodically reviewed and adjusted based on:
- New rules in Suricata.
- Wazuh rule updates.
- Analysis of new attack scenarios.
