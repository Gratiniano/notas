# NOTAS SOBRE RIA  
*10/05/2022*

El proposito es documentar los conocimientos y dudas que se tiene sobre la aplicación RIA para facilitar la elicitación de requisitos antes de escribir las *features* en Gherkin.

No hay de momento una estructura definida. Es más bien... tirar del hilo.

![fig](./_assets/under_construction.png)


## Referencias

##### [[Solicitudes]]
##### [[Expedientes]]
##### [[Empresas]]
##### [[Establecimientos]]
##### [[Actividad Económica]]

## Etiquetas
- #ADVERTENCIA Avisa de un concepto desconocido, ambiguo o extraño que podría resultar crítico.
- #DEFINICION  Define un concepto o entidad lo suficientemente importante como para merecer documentarse.
- #Nota Información anecdótica, interesante pero no crítica,
- #PENDIENTE Actividad o Consulta pendiente de hacerse.
- #FEATURE Indica una Característica en Gherkin
- ![fig](./_assets/Information_icon.png) información pertinente. Generalmente para introducir contexto.
- ![fig](./_assets/Red_question_icon.png) Destaca un concepto o cuestión que es necesario aclarar con otros miembros.

## Features
Los escenarios de las distintas #FEATURE se han clasificado con una serie de etiquetas para distinguir su propósito.

-  @API_REST. Escenario que serviría para la validación de un conjunto de datos sin implicaciones temporales o de interfaz.
-  @UI_Test. Escenario que serviría para la validación de una secuencia de acciones acciones (dado que seleccione algo puedo seleccionar otra cosa).  Util para modelar el comportamiento de una interfaz.

## Necesitas
Para visualizar correctamente los diagramas que acompañan al texto es necesario.
- Editor markdown [Obsidian](https://obsidian.md/).
- Plugin [Obsidian-Kroki]((https://github.com/gregzuro/obsidian-kroki)Permite renderizar los diagramas cómo imagen cuando se exporta el documento a PDF.
- Plugin  [Obsidian-PlantUML ](https://github.com/joethei/obsidian-plantuml) Permite definir diagrámas UML mediante descripciones textuales.

Los plugins indicados se instalan en Obsidian mediante la opción ***Settings -> Community plugins***.