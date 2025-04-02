# Detection Rules - OpenSOC Network Defense

## 🔎 Objective
Establish a set of custom rules for effective threat detection in the SOC environment.



## 🛡️ Custom Rules in Suricata

**File:** `/etc/suricata/rules/custom.rules`

### Rule Examples

➡️ [custom.rules](../../suricata/custom.rules)



## 🔧 Rules and Configuration in Wazuh

**File:** [/var/ossec/etc/ossec.conf](../../ossec/ossec.conf)

- Active-Response activation to block suspicious IPs in IPTables:
```xml
<active-response>
  <command>firewalldrop</command>
  <location>all</location>
  <level>10</level>
  <timeout>600</timeout>
</active-response>
```
**Custom rules:**  
➡️ [local_rules.xml](../../wazuh/local_rules.xml)

- Integrity and critical event rules:
  - Modification of critical files.
  - Changes in sensitive configurations.
  - Repeated failed access attempts.



## 🌐 Complement with Zeek and TShark

Zeek operates as a passive analyzer and logs:
- Suspicious connections.
- DNS and TLS analysis.
- Unusual port activity.

TShark used for targeted captures and forensic traffic analysis.
