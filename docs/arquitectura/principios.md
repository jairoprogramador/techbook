# Principios

## Encapsulación

Es el mecanismo que nos permite ocultar el estado de una unidad de codigo, con la finalidad de que actores externos no puedan modificarlo directamente.

La finalidad es evitar que cualquier agente externo modifique los datos directamente sin pasar un una capa que podamos controlar.

Ademas de proteger los datos, la encapsulacion tambien permite crear abstracciones de un componente para poder ser representado de la forma mas simple posible, ocultando los detalles irrelevantes para la arquitectura.

## Acoplamiento

Es el **nivel de dependencia** que existe entre unidades de codigo, es decir, indica hasta qué grado una unidad puede funcionar sin la otra.

El reto de un arquitecto no es suprimir todas las dependencias, ya que inevitablemente existiran, si no reducirlas al maximo; este reto no siempre sera posible y no debemos forzar una solucion para lograrlo.

El bajo acoplamiento se logra cuando un modulo no conoce o conoce muy poco sobre el funcionamiento interno de otros modulos. 

## Cohesión

Es el **grado de relacion** que tienen los elementos del modulo, es decir, la medida de union de los elementos de un modulo.

Mide que tan relacionados estan las unidades de codigo entre si, para cumplir con un unico objetivo o funcionalidad.

Busca que todos los componente de software que construyamos sean altamente cohesivos, es decir que el modulo este diseñado para resolver una unica problematica.
