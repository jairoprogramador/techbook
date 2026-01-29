# VM Sizes

## Analogía

VM Sizes es como elegir el tamaño de motor para tu auto según cómo lo vas a usar. Imagina que necesitas un vehículo: si solo vas a la tienda, un auto pequeño es suficiente. Si necesitas transportar carga pesada, necesitas una camioneta. Si necesitas velocidad máxima, necesitas un auto deportivo. VM Sizes funciona igual: Azure ofrece diferentes "tamaños" de VMs que son como diferentes configuraciones de motor. Cada tamaño tiene una combinación específica de CPU, memoria RAM, almacenamiento y ancho de banda de red. Para una aplicación web simple, un tamaño pequeño es suficiente. Para una base de datos grande, necesitas un tamaño grande con mucha memoria. Para procesamiento de video, necesitas un tamaño con GPU. Es como elegir el motor correcto para la tarea que necesitas realizar.

## Definición

VM Sizes son configuraciones predefinidas de recursos de cómputo (CPU, memoria, almacenamiento, red) que determinan el rendimiento y capacidad de una máquina virtual en Azure.

Permite:

- Elegir entre múltiples familias de tamaños optimizadas para diferentes cargas de trabajo
- Seleccionar configuración de CPU y memoria según requisitos de la aplicación
- Escalar verticalmente cambiando el tamaño de la VM según necesidades
- Optimizar costos eligiendo el tamaño adecuado para la carga de trabajo
- Acceder a tamaños especializados como GPU para procesamiento intensivo
- Configurar rendimiento de almacenamiento y red según el tamaño seleccionado
- Cambiar el tamaño de la VM cuando los requisitos cambian (requiere desasignación)

## Componentes

**vCPU** – Procesadores virtuales asignados a la VM que determinan capacidad de procesamiento.

**Memory (RAM)** – Memoria RAM disponible para la VM medida en GB.

**Temporary Storage** – Almacenamiento temporal local en la VM (no persistente).

**Data Disk Capacity** – Número máximo de discos de datos que se pueden conectar.

**Network Bandwidth** – Ancho de banda de red asignado medido en Gbps.

**VM Family** – Familia de tamaños optimizada para un tipo específico de carga de trabajo.

**General Purpose** – Familia de tamaños balanceada para CPU y memoria (B, Dsv3, Dv3).

**Compute Optimized** – Familia optimizada para CPU intensivo (Fsv2, Fs).

**Memory Optimized** – Familia optimizada para memoria (Esv3, Ev3, M).

**Storage Optimized** – Familia optimizada para alto rendimiento de disco (Lsv2, Ls).

**GPU** – Familia con unidades de procesamiento gráfico (NC, NCv2, ND, NV).

## Funcionalidad

1. Se selecciona una familia de VM según el tipo de carga de trabajo (General Purpose, Compute Optimized, etc.)
2. Se elige un tamaño específico dentro de la familia según requisitos de CPU, memoria y rendimiento
3. Azure asigna los recursos especificados (vCPU, RAM, almacenamiento, red) a la VM
4. El tamaño determina el costo de la VM (mayor tamaño = mayor costo)
5. Se puede cambiar el tamaño de la VM escalando verticalmente cuando los requisitos cambian
6. El cambio de tamaño requiere desasignar la VM (detener y liberar recursos)
7. Después del cambio, la VM se reinicia con la nueva configuración de recursos
8. Algunos cambios de tamaño pueden requerir migración a otro host físico
9. El rendimiento de almacenamiento y red está determinado por el tamaño seleccionado

## Casos de Uso

- Seleccionar tamaños General Purpose para aplicaciones web y servidores de aplicaciones estándar
- Usar tamaños Compute Optimized para cargas de trabajo intensivas en CPU como procesamiento de datos
- Elegir tamaños Memory Optimized para bases de datos grandes y análisis en memoria
- Implementar tamaños Storage Optimized para aplicaciones que requieren alto rendimiento de disco
- Usar tamaños GPU para machine learning, renderizado de video y procesamiento gráfico intensivo
- Optimizar costos seleccionando el tamaño mínimo necesario para la carga de trabajo
- Escalar verticalmente aumentando el tamaño cuando la aplicación requiere más recursos
- Reducir tamaño para ahorrar costos cuando los requisitos disminuyen

## Errores Comunes

- Pensar que todos los tamaños de VM tienen el mismo rendimiento (cada tamaño tiene recursos específicos)
- Confundir tamaño de VM con tamaño de disco (son conceptos separados)
- Creer que se puede cambiar el tamaño de una VM sin desasignarla (requiere desasignación y reinicio)
- Asumir que un tamaño mayor siempre es mejor (puede ser más costoso sin beneficio)
- Pensar que se puede reducir el tamaño de una VM sin límites (algunos cambios pueden no ser posibles)
- Confundir familias de VM (General Purpose vs Compute Optimized tienen diferentes optimizaciones)
- Creer que el tamaño determina solo CPU y memoria (también determina almacenamiento y red)
- Asumir que todos los tamaños están disponibles en todas las regiones (algunos tamaños son limitados)

## Preguntas

1. ¿Los VM Sizes son configuraciones predefinidas de CPU, memoria, almacenamiento y red que determinan el rendimiento?

2. ¿General Purpose es una familia de tamaños balanceada para aplicaciones estándar con CPU y memoria equilibradas?

3. ¿Memory Optimized es una familia optimizada para cargas de trabajo que requieren mucha RAM como bases de datos?

4. ¿Para cambiar el tamaño de una VM se requiere desasignarla (detener y liberar recursos) antes del cambio?

5. ¿Los tamaños GPU incluyen unidades de procesamiento gráfico para machine learning y renderizado?

6. ¿El tamaño de la VM determina el costo, con tamaños mayores siendo más costosos?

7. ¿Compute Optimized es una familia optimizada para cargas de trabajo intensivas en CPU?

8. ¿El rendimiento de almacenamiento y red está determinado por el tamaño de VM seleccionado?
