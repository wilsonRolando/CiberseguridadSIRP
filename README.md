## Plataforma Open Source de Respuesta a Incidentes (SIRP) con TheHive, Cortex, MISP, Elastic Stack, Wazuh
Implementación de una plataforma SIRP basada en TheHive, Cortex, MISP, Wazuh, ELK, Elasticsearch y Kibana para automatizar la detección, correlación y respuesta a incidentes de ciberseguridad.

SIRP es una plataforma diseñada para ayudar a los equipos de seguridad a manejar incidentes y responder de manera eficiente. Permite la integración de múltiples fuentes de datos, como sistemas de detección de intrusiones, herramientas de análisis de vulnerabilidades y otros sistemas de seguridad, para proporcionar una visión completa de los incidentes. Además, automatiza flujos de trabajo, lo que acelera las respuestas y mejora la eficiencia operativa

## Casos de uso
- Gestión de incidentes de seguridad.
- Integración de inteligencia de amenazas.
- Automatización de análisis mediante Cortex.
- Correlación de eventos mediante ElastAlert.
- Implementación de laboratorios SOC y DFIR.

## Tecnologías
- TheHive
- Cortex
- MISP
- Elasticsearch
- Kibana
- ElastAlert
- Filebeat
- Docker
- Wazuh
- Ubuntu
- Linux
  
Este proyecto utiliza herramientas open source para proporcionar una plataforma flexible, escalable y accesible, permitiendo a las organizaciones mejorar su capacidad para detectar, gestionar y mitigar incidentes de seguridad en tiempo real.
!["diagrama"](https://github.com/wilsonRolando/CiberseguridaSIRP/blob/main/infraestructura.png)

### Requerimientos 
- Docker 20.10 +
- Docker-compose 1.29 +
- Ubuntu 20.04
- 16 GB RAM +
- 8 vCPUs +

### Instalación
* Modificar el archivo *.env* , variable de entorno IP_PUBLICA, para desplegar en un entorno local ingresar la ip del host.
* En el directorio *CiberseguridaSIRP/*,  ejecutar:
```yaml
docker-compose -f 1.docker-compose.yml up -d
```
```shell
./2.permission-script.sh
```
```shell
./3.AnalyzerResponder-script.sh
```
```shell
./4.kibanaWuazuh-Plugin.sh
```

### Integración 
- En cortex y MISP, generar la api-key de un usuario y remplazar en el campo *key* del archivo *thehive/application.conf*, también remplazar la ip del campo *url* de la sección de MISP
- Reiniciar thehive
```yaml
docker restart thehive
```
- En thehive, generar el api-key de un usuario con permisos de crear alertas y remplazar en la regla elastAlert/rule/rule-test.yml

### Test
- Descargar filebeat,  configurar el archivo filebeat.yml, en el directorio test se encuentra una muestra de configuración del archivo filebeat.yml  con un test.log de prueba.
- Ejecutar filebeat, e ingresar registros en el test.log, si todo esta correcto, los registros se observa en kibana, y al ingresar más de dos registros repetidos continuos, se generan alertas en thehive. 

### Puertos
- Elasticsearch
http://localhost:9200
- Kibana
http://localhost:5601
- Thehive
http://localhost:9000
- Cortex
http://localhost:9001
- MISP
http://localhost
  - usuario: **admin@admin.test**
  - clave: **admin**


