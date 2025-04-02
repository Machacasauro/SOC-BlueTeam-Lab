# Detection Rules - OpenSOC Network Defense

## 🔎 Objetivo
Establecer un conjunto de reglas personalizadas para la detección eficaz de amenazas en el entorno del SOC.

---

## 🛡️ Reglas Personalizadas en Suricata

**Archivo:** `/etc/suricata/rules/custom.rules`

### Ejemplos de Reglas

➡️ [custom.rules](../../suricata/custom.rules)
```
---

## 🔧 Reglas y Configuración en Wazuh

**Archivo:** `/var/ossec/etc/ossec.conf`

- Activación de Active-Response para bloqueo de IPs sospechosas en IPTables:
```xml
<active-response>
  <command>firewalldrop</command>
  <location>all</location>
  <level>10</level>
  <timeout>600</timeout>
</active-response>
```
## Reglas personalizadas

Puedes consultar las reglas locales de Wazuh aquí:

➡️ [local_rules.xml](../../wazuh/local_rules.xml)
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