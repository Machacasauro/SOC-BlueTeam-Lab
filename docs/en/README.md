# Complete Project: Implementation of a SOC with Suricata, Wazuh, ELK Stack, and Incident Simulation

## Objective

Develop a functional environment for threat detection and incident response using open-source tools to simulate a real Security Operations Center (SOC) environment.

## Description

Blue Team Lab is a personal and professional project where I have designed, implemented, and managed a complete threat detection and response environment based on Open Source technologies. All systems have been installed, configured, and manually customized without using preconfigured distributions.

This lab aims to demonstrate my technical capabilities in cybersecurity infrastructure management, incident analysis, and threat response in corporate environments.

## Relevant Certifications and Training

- Cisco Cybersecurity Operations Fundamentals (200-201 CBROPS)
- TryHackMe SOC Level 1
- Mikrotik RouterOS 7.12 Certifications (MTCNA, MTCRE, MTCWE) - Perimeter firewall rules, QoS, and VLAN

## 📚 Project Index

1. Project Architecture
2. Technical Implementation
3. Attack Scenarios Simulation
4. Event Analysis and Correlation
5. Automation and Vulnerability Management
6. Threat Intelligence (CTI/OSINT)
7. Digital Forensics and Incident Response (DFIR)
8. Technical Documentation and Playbooks
9. Complementary and Future Certifications

---

## 1. Project Architecture

[Installation Guide](installation-guide.md)

**Environment:**

- OS: Ubuntu Server 22.04 LTS (Apache Server, MySQL, Documentation) Lab
- IDS/IPS: Suricata
- SIEM: ELK Stack (Elasticsearch, Logstash, Kibana)
- EDR: Wazuh
- Additional tools: Kali Linux (Hydra, Nmap, TryHackMe Labs, Zeek, TShark)
- DFIR: REMnux v7

**Architecture Diagram:**

- Suricata: Monitors network traffic in IDS mode, generating alerts.
- Filebeat: Collects Suricata logs and sends them to Logstash.
- Logstash: Parses and enriches logs.
- Elasticsearch: Stores the events.
- Kibana: Visualizes and analyzes the data.
- Wazuh: Correlates events, integrates with Filebeat and Active-Response.
- Zeek & TShark: Passive and forensic network traffic analysis.

---

## 2. Technical Implementation

[Dashboards Setup](dashboards-setup.md)

### Installation and Configuration of Elastic Stack

- Elasticsearch, Logstash, and Kibana installed from official repositories.
- Customized pipeline and dashboard configuration.

### Integration and Verification

- Confirm that logs flow correctly.
- Review dashboards in Kibana.

---

## 3. Attack Scenarios Simulation

[Attack Simulation](attack-simulation.md)

---

## 4. Event Analysis and Correlation

[Detection Rules](detection-rules.md)

- Review Suricata alerts in Kibana.
- Event correlation via Wazuh.
- Use of TShark and Zeek for passive analysis.

---

## 5. Automation and Vulnerability Management

- Automation of rule deployment.
- Generation of weekly reports.
- Use of OpenVAS for vulnerability scanning.

---

## 6. Threat Intelligence (CTI/OSINT)

- Integration of OSINT sources:
  - AbuseIPDB

---

## 7. Digital Forensics and Incident Response (DFIR)

- Extraction and analysis of logs post-incident.
- Use of Wireshark, Zeek, and Volatility for advanced investigation.

---

## 8. Technical Documentation and Playbooks

- Detailed procedures for:
  - Installation of each component.
  - Incident response.
  - Forensic analysis.

---

## 9. Complementary and Future Certifications

- Upcoming Certification: Security Analyst Level 1 (SAL1) :shield:
- Active preparation for: eJPT v2 (INE Security) :crossed_swords:
- Objective: Purple Team :crossed_swords: :shield:

---

## 📅 Troubleshooting and Issues Solved

- Incorrect configuration in suricata.yaml: Solved by verifying syntax and using `suricata -T`.
- Connection issues between Filebeat and Logstash: Resolved by adjusting ports and YAML configuration.
- Wazuh agent not sending logs: Fixed by adjusting keys and verifying connectivity.
- Parsing error in Logstash: Reviewed and corrected grok patterns.
- Integration issues between Kibana and Wazuh: Resolved by installing the correct plugin and adjusting roles.
