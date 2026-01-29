# Availability Zones

## Analogía

Availability Zones es como tener copias de tu servidor en edificios completamente diferentes en la misma ciudad, cada uno con su propia electricidad, agua y conexiones. Imagina que tienes un servidor crítico y quieres máxima protección. En lugar de tenerlo solo en un edificio, lo duplicas y pones cada copia en edificios diferentes que están separados por varios kilómetros. Cada edificio tiene su propia infraestructura independiente: electricidad, agua, Internet, todo separado. Si un edificio tiene un problema (corte de luz, incendio, terremoto), los otros edificios siguen funcionando. Availability Zones funciona igual: son zonas físicas separadas dentro de la misma región, cada una con su propia infraestructura independiente. Si una zona falla completamente, tus VMs en otras zonas siguen operando. Es el nivel más alto de protección dentro de una región.

## Definición

Availability Zones son ubicaciones físicas separadas dentro de una región de Azure, cada una con su propia fuente de alimentación, red y refrigeración independientes, diseñadas para proporcionar alta disponibilidad y protección contra fallos a nivel de zona.

Permite:

- Distribuir VMs en múltiples zonas físicas separadas dentro de la misma región
- Proteger contra fallos de infraestructura a nivel de zona (cortes de luz, fallos de red)
- Garantizar que al menos una zona esté disponible si otra falla completamente
- Reducir latencia comparado con múltiples regiones (misma región, diferentes zonas)
- Cumplir con requisitos de alta disponibilidad y resiliencia empresarial
- Implementar aplicaciones zone-redundant que se replican automáticamente entre zonas
- Proteger contra desastres locales dentro de una región

## Componentes

**Availability Zone** – Zona física separada dentro de una región con infraestructura independiente (1, 2 o 3).

**Zonal Deployment** – VM desplegada en una zona específica (zona 1, 2 o 3).

**Zone-Redundant** – Recurso replicado automáticamente en múltiples zonas (Load Balancer, Storage).

**Region** – Área geográfica que contiene múltiples Availability Zones (3 zonas por región soportada).

**Infraestructura Independiente** – Cada zona tiene su propia fuente de alimentación, red y refrigeración.

**SLA 99.99%** – Acuerdo de nivel de servicio para VMs distribuidas en múltiples Availability Zones.

**Latencia Inter-Zona** – Latencia de red entre zonas dentro de la misma región (menor que entre regiones).

## Funcionalidad

1. Una región de Azure contiene múltiples Availability Zones (típicamente 3) que son zonas físicas separadas.
2. Cada zona tiene infraestructura completamente independiente: alimentación, red, refrigeración.
3. Se despliegan VMs en zonas específicas (zonal) o de forma zone-redundant según los requisitos.
4. Azure distribuye automáticamente los recursos zone-redundant en múltiples zonas.
5. Si una zona falla completamente (corte de luz, fallo de red), las otras zonas continúan operando.
6. Los recursos zone-redundant como Load Balancers y Storage se replican automáticamente entre zonas.
7. La latencia entre zonas dentro de la misma región es menor que entre diferentes regiones.
8. Azure garantiza un SLA de 99.99% cuando las VMs están distribuidas en múltiples Availability Zones.
9. Las aplicaciones pueden implementarse para ser resilientes a fallos de zona mediante distribución en múltiples zonas.

## Casos de Uso

- Implementar alta disponibilidad para aplicaciones críticas distribuyendo VMs en múltiples zonas.
- Proteger contra fallos de infraestructura a nivel de zona (cortes de luz, fallos de red).
- Cumplir con requisitos de SLA de 99.99% para aplicaciones empresariales críticas.
- Implementar aplicaciones zone-redundant que se replican automáticamente entre zonas.
- Reducir latencia comparado con múltiples regiones manteniendo alta disponibilidad.
- Proteger contra desastres locales dentro de una región sin necesidad de múltiples regiones.
- Implementar arquitecturas de alta disponibilidad para bases de datos y aplicaciones críticas.
- Cumplir con requisitos de compliance que exigen distribución geográfica dentro de una región.

## Errores Comunes

- Pensar que Availability Zones están en diferentes regiones (están en la misma región, diferentes zonas físicas).
- Confundir Availability Zones con Availability Sets (Availability Zones son zonas físicas separadas, Availability Sets son dominios lógicos).
- Creer que todas las regiones tienen Availability Zones (solo algunas regiones las soportan).
- Asumir que una VM puede estar en múltiples zonas simultáneamente (una VM está en una zona específica).
- Pensar que Availability Zones protegen contra desastres regionales (solo protegen contra fallos de zona dentro de la región).
- Confundir zonal deployment con zone-redundant (zonal deployment es una zona específica, zone-redundant es múltiples zonas).
- Creer que se puede mover una VM entre zonas sin recrearla (requiere recrear la VM en la nueva zona).
- Asumir que Availability Zones tienen la misma latencia que Availability Sets (Availability Zones tienen mayor latencia entre ellas).

## Preguntas

1. ¿Availability Zones son zonas físicas separadas dentro de la misma región, cada una con infraestructura independiente?.

2. ¿Cada Availability Zone tiene su propia fuente de alimentación, red y refrigeración independientes?.

3. ¿Azure garantiza un SLA de 99.99% cuando las VMs están distribuidas en múltiples Availability Zones?.

4. ¿Una VM puede estar desplegada en una zona específica (zonal) o los recursos pueden ser zone-redundant?.

5. ¿Availability Zones protegen contra fallos de infraestructura a nivel de zona pero no contra desastres regionales?.

6. ¿Los recursos zone-redundant como Load Balancers se replican automáticamente en múltiples zonas?.

7. ¿La latencia entre Availability Zones dentro de la misma región es menor que entre diferentes regiones?.

8. ¿No todas las regiones de Azure tienen Availability Zones disponibles?.
