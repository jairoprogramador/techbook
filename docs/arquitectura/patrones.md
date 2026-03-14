# ¿Qué son los Patrones?

Un patron es un modelo que sirve de muestra para sacar cosas similares. Si hablamos de tecnologia, un patron es una solución que se puede reutilizar para resolver problemas comunes.

### Componente de Software

Un componente es una unidad conceptual, codigo cohesionado con una sola responsabilidad bien definida, que expone una interface de comunicacion. 

## Patrones Arquitectonicos

Son soluciones reutilizables a problemas de arquitectura. Analiza estricciones tecnologicas, hardware, performace, seguridad, etc. Tambien se centra en los componentes como un todo, su comportamiento, relacion, comunicacion entre ellos. Este tipo de desiciones tiene un impacto global sobre la aplicacion ya que se centra en la estructura como un todo.

Define las reglas de juego de todo un sistema.

**Preguntas típicas de arquitectura**:

- ¿Cómo separo la lógica de negocio de la infraestructura técnica?
- ¿El sistema debe ser un monolito o varios servicios independientes?
- ¿Cómo se comunican entre sí las distintas partes del sistema?
- ¿Dónde vive cada tipo de responsabilidad a nivel global?

## Patrones de Diseño

Son soluciones reutilizables a problemas de diseño, que tienen un impacto menor en los componentes y que se enfocados en clases y objetos.

- **Patrones Creacionales**: Para la creacion y construccion de objetos
- **Patrones Estructurales**: La forma en que unas clases se relacionan con otras
- **Patrones de Comportamiento**: Procedimientos y asignacion de responsabilidades a los objetos.

Los patrones de diseño se enfoca en problemas (**problema de diseño**) que aparece dentro de un componente o en la relación directa entre ellos. Se refiere a cómo estructurar el código para que sea **flexible, mantenible y fácil de entender** a pequeña escala.

Es como juegas siguiendo las reglas globales (patron arquitectonico) dentro de cada componente.

**Preguntas típicas de diseño**:

- ¿Cómo permito que este componente cambie su comportamiento sin modificar su código?
- ¿Cómo evito que esta clase tenga demasiadas responsabilidades?
- ¿Cómo hago que estos dos objetos colaboren sin acoplarse fuertemente?
