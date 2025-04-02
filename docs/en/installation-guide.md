# Installation Guide - OpenSOC Network Defense

## 🔧 Objective
Provide detailed steps for installing and configuring the main components of the OpenSOC Network Defense environment.

---

## 1. System Requirements

- Ubuntu Server 22.04 LTS
- Minimum 8 GB RAM
- 4 vCPU
- 80 GB storage

---

## 2. Installation of Elastic Stack (Elasticsearch, Logstash, Kibana)

### Installation
```bash
sudo apt update && sudo apt upgrade -y
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-8.x.list
sudo apt update
sudo apt install elasticsearch logstash kibana -y
```

### Configuration
- Elasticsearch: [/etc/elasticsearch/elasticsearch.yml](../../Elasticsearch/elasticsearch.yml)
- Logstash: [/etc/logstash/conf.d/filebeat.conf](../../Logstash/conf.d/filebeat.conf)
- Kibana: [/etc/kibana/kibana.yml](../../kibana/kibana.yml)

Start services:
```bash
sudo systemctl enable elasticsearch logstash kibana
sudo systemctl start elasticsearch logstash kibana
```

---

## 3. Installation and configuration of Suricata

### Installation
```bash
sudo apt update
sudo apt install suricata -y
```

### Execution
Manual:
```bash
sudo suricata -i enp0s3 -c /etc/suricata/suricata.yaml --af-packet
```
Service (Recommended):
```bash
sudo systemctl enable suricata
sudo systemctl start suricata
```
---

## 4. Installation and configuration of Filebeat

### Installation
```bash
sudo apt update
sudo apt install filebeat -y
sudo filebeat modules enable suricata
```

### Configuration
File: [/etc/filebeat/filebeat.yml](../../Filebeat/filebeat.yml)
```yaml
output.logstash:
  hosts: ["localhost:5044"]
```

Start:
```bash
sudo systemctl start filebeat
sudo systemctl enable filebeat
```

---

## 5. Installation and configuration of Wazuh

### Installation
Follow the official guide:
https://documentation.wazuh.com/current/installation-guide/index.html

Configure integration with Kibana and Filebeat.

---

## 6. Installation of Zeek (Complementary)

```bash
sudo apt update
sudo apt install zeek -y
sudo zeekctl deploy
```
Zeek operates as an independent system.

---

## 7. Installation of TShark (Complementary)

**TShark** is used as an auxiliary tool for on-demand traffic capture and forensic network analysis.

### Installation
```bash
sudo apt update
sudo apt install tshark -y
```

### Basic Usage
Capture traffic on the main network interface:
```bash
sudo tshark -i enp0s3 -w /home/soc/captures/capture.pcap
```

Filter HTTP packets:
```bash
tshark -r capture.pcap -Y "http"
```

**Note:** TShark is not integrated into ELK or Wazuh. Its use is manual for specific validation and analysis.

---

## 8. Troubleshooting

| Issue | Solution |
|:-:|:-:|
| Syntax error in suricata.yaml | Verify and correct using `suricata -T` |
| Failed connection between Filebeat and Logstash | Check ports and output configuration in filebeat.yml |
| Parsing issue in Logstash | Review and correct grok patterns |
| Wazuh agent not reporting | Check key and connectivity |
| Wazuh plugin in Kibana not loading | Check version and proper installation |

---

## 9. Verification
- Confirm that Suricata logs appear in Kibana.
- Verify that Wazuh events are active.
- Check Zeek and TShark captures.
