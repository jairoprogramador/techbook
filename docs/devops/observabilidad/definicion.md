# Definición

La observabilidad responde: **¿Por qué no está funcionando?**

Su objetivo es que puedas comprender qué está ocurriendo dentro del sistema, incluso cuando el problema nunca había ocurrido antes.

Se basa principalmente en tres pilares:

## 1. Métricas

Datos numéricos agregados.

Ejemplos:

- Latencia
- CPU
- Memoria
- Requests por segundo
- Errores por minuto

Herramientas para almacenar:

- Prometheus
- CloudWatch: servicio de AWS para almacenar logs y metricas

## 2. Logs

Eventos detallados que ocurren en la aplicación.

Ejemplo:

- Usuario 452 inició sesión
- Pedido 987 creado
- Error al conectar con PostgreSQL

Con un buen sistema de logs puedes filtrar por:

- usuario
- request
- servicio
- nivel (INFO, WARN, ERROR)

Herramientas para almacenar:

- CloudWatch
- Loki
- Logstash

## 3. Trazas

Muestran el recorrido completo de una petición entre múltiples servicios. Una traza permite saber exactamente cuánto tardó cada componente. Sin trazas solo verías que la petición tardó 962 ms, pero no dónde se consumió el tiempo.

Herramientas para almacenar:

- Tempo

# Dashboard

Es una interfaz visual que centraliza, analiza y muestra indicadores clave de desempeño (KPI) y datos en tiempo real. Su objetivo es sintetizar información compleja para facilitar la rápida toma de decisiones sin perderse en el volumen de datos.

Existen herramientas que usan los datos almacenados de las metricas, logs y trazas para mostrar dashboard amigables.

- Grafana
- Kibana

Otras herramientas de obsevabilidad empresarial que hacen todo en uno, almacenan y crean dashboards

- ELK (Elasticsearch Logstash Kibana)
- Datadog
- New Relic
- Dynatrace