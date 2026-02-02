# Azure Cost Management

## Analogía

Azure Cost Management es como el panel de gastos de tu organización en la nube: ves cuánto se gasta por suscripción, por grupo de recursos, por recurso o por etiqueta. Puedes definir presupuestos y recibir alertas cuando te acercas al límite. No es donde pagas; es donde analizas el consumo, identificas tendencias y controlas el gasto. Funciona con suscripciones de Azure y también con ofertas como Microsoft Customer Agreement o Contrato Enterprise para tener una vista unificada del costo.

## Definición

Azure Cost Management (antes Cost Management + Billing en el portal) es el conjunto de capacidades de Azure para analizar, supervisar y optimizar el gasto en recursos de Azure: informes de costos por suscripción, grupo de recursos, recurso o etiqueta; presupuestos y alertas; recomendaciones de optimización; y exportación de datos para análisis externo.

Permite:

- Visualizar costos por suscripción, grupo de recursos, recurso, servicio o etiqueta
- Crear presupuestos y configurar alertas cuando el gasto se acerca o supera un umbral
- Analizar tendencias de costo en el tiempo (diario, mensual, acumulado)
- Exportar datos de costos a una cuenta de almacenamiento o a un workspace de Log Analytics
- Recibir recomendaciones de optimización (p. ej. recursos infrautilizados, reservas)
- Filtrar y agrupar costos por etiquetas para asignación de gasto por departamento o proyecto

## Componentes

**Análisis de costos** – Vista interactiva que permite filtrar, agrupar y segmentar costos por suscripción, grupo de recursos, recurso, servicio, etiqueta o período

**Presupuestos** – Límites de gasto configurados por suscripción, grupo de recursos o grupo de administración; se pueden definir alertas al alcanzar umbrales (p. ej. 80 %, 100 %)

**Alertas de presupuesto** – Notificaciones (correo, Action Group) cuando el costo se acerca o supera el umbral definido en el presupuesto

**Exportación de costos** – Programación de exportación de datos de costos a una cuenta de almacenamiento de Azure o a un workspace de Log Analytics para reporting o análisis externo

**Recomendaciones** – Sugerencias de optimización (p. ej. comprar reservas, redimensionar o apagar recursos infrautilizados)

**Asignación de costos (por etiquetas)** – Agrupación de costos por etiquetas para asignar gasto a departamentos, proyectos o entornos

## Funcionalidad

1. Se accede a Cost Management desde el portal de Azure (o desde el centro de costos de la facturación)
2. Se visualizan costos por suscripción, grupo de recursos, recurso, servicio o etiqueta; se filtran por período (mes actual, último mes, personalizado)
3. Se crean presupuestos por suscripción, grupo de recursos o grupo de administración con umbrales (p. ej. 80 %, 100 %) y alertas (correo, Action Group)
4. Cuando el gasto alcanza el umbral, se disparan las alertas configuradas
5. Se pueden exportar datos de costos de forma programada a una cuenta de almacenamiento o a Log Analytics
6. Se revisan recomendaciones de optimización (reservas, right-sizing) para reducir gasto
7. Se agrupan costos por etiquetas para asignar gasto a departamentos o proyectos cuando los recursos están etiquetados

## Casos de Uso

- Supervisar el gasto por suscripción, grupo de recursos o recurso para control de costos
- Crear presupuestos y alertas para evitar sobrepasos (p. ej. alerta al 80 % del presupuesto mensual)
- Asignar costos a departamentos o proyectos agrupando por etiquetas
- Exportar datos de costos a almacenamiento o Log Analytics para reporting o dashboards externos
- Identificar recursos infrautilizados o oportunidades de reservas mediante recomendaciones
- Analizar tendencias de costo en el tiempo para planificación y forecasting

## Errores Comunes

- Confundir Cost Management con la facturación o el método de pago (Cost Management es análisis y supervisión; la facturación y el pago se gestionan en la sección de facturación de la suscripción o del contrato)
- Pensar que los presupuestos bloquean el gasto (los presupuestos solo envían alertas; no detienen la creación de recursos ni el consumo)
- Creer que los costos se asignan automáticamente por etiquetas sin etiquetar recursos (hay que etiquetar recursos para que el costo se agrupe por etiqueta)
- Asumir que Cost Management está disponible en todas las ofertas sin restricciones (algunas capacidades dependen del tipo de oferta o del rol)
- Olvidar que las alertas de presupuesto requieren configurar destinatarios (correo o Action Group) para recibir notificaciones

## Preguntas

1. ¿Azure Cost Management permite analizar y supervisar el gasto en recursos de Azure por suscripción, grupo de recursos o recurso?

2. ¿Los presupuestos en Cost Management envían alertas cuando se alcanza un umbral pero no bloquean el gasto ni la creación de recursos?

3. ¿Se pueden exportar datos de costos de forma programada a una cuenta de almacenamiento o a Log Analytics?

4. ¿Para asignar costos por departamento o proyecto hay que etiquetar los recursos y luego agrupar por etiqueta en el análisis de costos?

5. ¿Las recomendaciones de Cost Management pueden incluir sugerencias de reservas o redimensionamiento de recursos?

6. ¿Las alertas de presupuesto requieren configurar destinatarios (correo o Action Group) para recibir notificaciones?
