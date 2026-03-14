#Monolito

Es un estilo que consiste en crear una aplicacion autosuficiente que contenga absolutamente toda la funcionalidad necesaria para la cual fue diseñada, sin dependencias externas que complementen su funcionalidad, es decir, es una unidad cohesiva de codigo.

Puede se una sola unidad de codigo o creada a partir de varios modulos o librerias, pero lo que la distingue es que **al momento de compilar se empaqueta como una sola pieza**, de tal forma que todos los modulos y librerias se empaquetan juntos con la aplicacion principal.

###Caracteristicas: 

- Son autosuficientes
- Realizan una tarean de principio a final.
- Por lo general son grandes
- Por lo general son silos de datos
- Todo el sistema corre sobre una sola plataforma

###Ventajas:

- Fácil de desarrollar
- Fácil de escalar
- Pocos puntos de fallo
- Autónomo
- Mejor performance
- Fácil de probar

### Desventajas

- Depende de un Stack tecnológico
- Escalado costoso en terminos de recursos
- Mantenimiento multi equipo complejo
- Unico punto de fallo
- La separacion de responsabilidades depende exclusivamente del código
