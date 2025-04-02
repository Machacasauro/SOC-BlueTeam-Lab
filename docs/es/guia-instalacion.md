# Guía de instalación - OpenSOC Network Defense

## 🔧 Objetivo
Proporcionar los pasos detallados para la instalación y configuración de los componentes principales del entorno OpenSOC Network Defense.



## 1. Requisitos del Sistema

- Ubuntu Server 22.04 LTS
- 8 GB RAM mínimo
- 4 vCPU
- 80 GB de almacenamiento



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
- Logstash: [/etc/logstash/conf.d/filebeat.conf](../../Logstash/conf.d/filebeat.conf)
- Kibana: [/etc/kibana/kibana.yml](../../kibana/kibana.yml)

Iniciar servicios:
```bash
sudo systemctl enable elasticsearch logstash kibana
sudo systemctl start elasticsearch logstash kibana
```


## 3. Instalación y configuración de Suricata

### Instalación
```bash
sudo apt update
sudo apt install suricata -y
```

### Ejecución
Manual:
```bash
sudo suricata -i enp0s3 -c /etc/suricata/suricata.yaml --af-packet
```

Servicio (Recomendado):
```bash
sudo systemctl enable suricata
sudo systemctl start suricata
```


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

Servicio:
```bash
sudo systemctl start filebeat
sudo systemctl enable filebeat
```



## 5. Instalación y configuración de Wazuh

### Instalación
Seguir la guía oficial:
https://documentation.wazuh.com/current/installation-guide/index.html

Configurar integración con Kibana y Filebeat.



## 6. Instalación de Zeek (Complementario)

```bash
sudo apt update
sudo apt install zeek -y
sudo zeekctl deploy
```
Zeek opera como sistema independiente.


## 7. Instalación de TShark (Complementario)

**TShark** se utiliza como herramienta auxiliar para capturas y análisis forense de tráfico de red.

### Instalación
```bash
sudo apt update
sudo apt install tshark -y
```

### Uso básico
Captura de tráfico en la interfaz principal:
```bash
sudo tshark -i enp0s3 -w /home/ubuntu/capturas/captura.pcap
```

Filtrado de paquetes HTTP:
```bash
tshark -r captura.pcap -Y "http"
```

**Nota:** No está integrado directamente en ELK o Wazuh. Su uso es manual para validación puntual.


## 8. Troubleshooting

| Problema | Solución |
|:-:|:-:|
| Error de sintaxis en suricata.yaml | Verificar y corregir con `suricata -T` |
| Conexión fallida entre Filebeat y Logstash | Revisar puertos y configuración de salida en filebeat.yml |
| Problema de parsing en Logstash | Revisar y corregir grok patterns |
| Wazuh agent no reporta | Verificar clave y conectividad |
| Plugin Wazuh en Kibana no carga | Comprobar versión e instalación correcta |



## 9. Verificación
- Confirmar que los logs de Suricata aparecen en Kibana.
- Verificar que los eventos de Wazuh están activos.
- Comprobar capturas de Zeek y TShark.

