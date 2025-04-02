# Installation Guide - OpenSOC Network Defense

## 🔧 Objetivo
Proporcionar los pasos detallados para la instalación y configuración de los componentes principales del entorno OpenSOC Network Defense.

---

## 1. Requisitos del Sistema

- Ubuntu Server 22.04 LTS
- 8 GB RAM mínimo
- 4 vCPU
- 80 GB de almacenamiento

---

## 2. Instalación de Elastic Stack (Elasticsearch, Logstash, Kibana)

### Instalación
```bash
sudo apt update && sudo apt upgrade -y
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-8.x.list
sudo apt update
sudo apt install elasticsearch logstash kibana -y
```

### Configuración
- Elasticsearch: [/etc/elasticsearch/elasticsearch.yml](../../Elasticsearch/elasticsearch.yml)
- Logstash: [/etc/logstash/conf.d/](../../Logstash/conf.d/filebeat.conf)
- Kibana: [/etc/kibana/kibana.yml](../../kibana/kibana.yml)
```

Iniciar servicios:
```bash
sudo systemctl enable --now elasticsearch logstash kibana
```

---

## 3. Instalación y configuración de Suricata

### Instalación
```bash
sudo apt update
sudo apt install suricata -y
```

### Ejecución
```bash
sudo suricata -i enp0s3 -c /etc/suricata/suricata.yaml --af-packet
```

---

## 4. Instalación y configuración de Filebeat

### Instalación
```bash
sudo apt update
sudo apt install filebeat -y
sudo filebeat modules enable suricata
```

### Configuración
Archivo: [/etc/filebeat/filebeat.yml](../../Filebeat/filebeat.yml)
```yaml
output.logstash:
  hosts: ["localhost:5044"]
```

Inicio:
```bash
sudo systemctl start filebeat
sudo systemctl enable filebeat
```

---

## 5. Instalación y configuración de Wazuh

### Instalación
Seguir la guía oficial:
https://documentation.wazuh.com/current/installation-guide/index.html

Configurar integración con Kibana y Filebeat.

---

## 6. Instalación de Zeek

```bash
sudo apt update
sudo apt install zeek -y
sudo zeekctl deploy
```
Zeek opera como sistema independiente.

---

## 7. Troubleshooting

| Problema | Solución |
|:-:|:-:|
| Error de sintaxis en suricata.yaml | Verificar y corregir con `suricata -T` |
| Conexión fallida entre Filebeat y Logstash | Revisar puertos y configuración de salida en filebeat.yml |
| Problema de parsing en Logstash | Revisar y corregir grok patterns |
| Wazuh agent no reporta | Verificar clave y conectividad |
| Plugin Wazuh en Kibana no carga | Comprobar versión e instalación correcta |

---

## 8. Verificación
- Confirmar que los logs de Suricata aparecen en Kibana.
- Verificar que los eventos de Wazuh están activos.
- Comprobar capturas de Zeek y TShark.