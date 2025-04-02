# Attack Simulation - OpenSOC Network Defense

## 🔎 Objective
Simulate attack scenarios in a controlled environment to validate the effectiveness of detection and response solutions implemented in the OpenSOC Network Defense project.



## 🔫 Simulated Attack Scenarios

### 1. SSH Brute Force Attack
- **Tool:** Hydra
- **Command executed:**
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.10.5
```
- **Expected result:**
  - Alert in Suricata and Wazuh.
  - Correlated event in Kibana.
  - Automatic IP blocking in Wazuh Active-Response.



### 2. Port Scanning with Nmap
- **Tool:** Nmap
- **Command executed:**
```bash
nmap -sS -p 1-65535 192.168.10.5
```
- **Expected result:**
  - SYN scan detection by Suricata.
  - Event registration in Wazuh and visualization in Kibana.
  - Detailed logs in Zeek.



### 3. SQL Injection
- **Tool:** SQLMap
- **Command executed:**
```bash
sqlmap -u "http://192.168.10.5/vuln.php?id=1" --risk=3 --level=5 --batch
```
- **Expected result:**
  - Detection by Suricata using HTTP rules.
  - Event logged in Wazuh.
  - Complementary analysis in TShark and Zeek.



### 4. ICMP DoS Attack
- **Tool:** hping3
- **Command executed:**
```bash
hping3 -1 --flood -V 192.168.10.5
```
- **Expected result:**
  - Detection by Suricata and Wazuh.
  - Event visualized in Kibana.



## 🔎 Complementary Analysis
- **TShark:** Used to capture and analyze packets during attacks.
- **Zeek:** Generates network activity logs for detailed analysis.



## 📅 Detection Validation
Each simulated attack has been validated by verifying:
- Proper generation of alerts in Suricata and Wazuh.
- Event correlation in Kibana.
- Traffic capture in Zeek and TShark.
- Application of automatic response (when applicable).
