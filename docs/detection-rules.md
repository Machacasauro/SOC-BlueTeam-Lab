# Detection Rules - OpenSOC Network Defense

## 🔎 Objetivo
Establecer un conjunto de reglas personalizadas para la detección eficaz de amenazas en el entorno del SOC.

---

## 🛡️ Reglas Personalizadas en Suricata

**Archivo:** `/etc/suricata/rules/custom.rules`

### Ejemplos de Reglas

1. **SSH Brute Force Detection**
```bash
alert tcp any any -> any 22 (msg:"SSH Brute Force Detected"; threshold:type both, track by_src, count 5, seconds 60; sid:1000001;)
```

2. **HTTP GET Flood**
```bash
alert tcp any any -> any 80 (msg:"HTTP GET Flood Detected"; flow:to_server,established; content:"GET"; http_method; threshold:type both, track by_src, count 20, seconds 10; sid:1000002;)
```

3. **MySQL Brute Force Detection**
```bash
alert tcp any any -> any 3306 (msg:"MySQL Brute Force Detected"; flow:to_server,established; content:"Access denied"; nocase; threshold:type both, track by_src, count 5, seconds 60; sid:1000004;)
```

4. **ICMP DoS Attack**
```bash
alert icmp any any -> any any (msg:"ICMP DoS Attack Detected"; itype:8; threshold:type both, track by_src, count 50, seconds 10; sid:1000005;)
```

5. **Jumbo Frames Detection**
```bash
alert ip any any -> any any (msg:"Jumbo Frames Detected"; dsize:>9000; sid:1000006;)
```

---

## 🔧 Reglas y Configuración en Wazuh

**Archivo:** `/var/ossec/etc/ossec.conf`

- Activación de Active-Response para bloqueo de IPs sospechosas:
```xml
<active-response>
  <command>firewalldrop</command>
  <location>all</location>
  <level>10</level>
  <timeout>600</timeout>
</active-response>
```

- Reglas de integridad y eventos críticos:
  - Modificación de archivos críticos.
  - Cambios en configuraciones sensibles.
  - Accesos fallidos reiterados.

---

## 🌐 Complemento con Zeek y TShark

Zeek opera como analizador pasivo y registra:
- Conexiones sospechosas.
- Análisis de DNS y TLS.
- Actividad inusual en puertos.

TShark utilizado para capturas puntuales y análisis forense de tráfico.

