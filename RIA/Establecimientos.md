
# Establecimientos
#DEFINICION *Industria -* Conjunto de instalaciones dedicadas a una actividad económica. En nuestro caso estarán determinadas por su relación con una  persona física ó jurídica.

#DEFINICION *Establecimiento -* Cada una de las instalaciones dedicadas a la realización de una actividad economica concreta y para una empresa determinada a través de una relación de tenencia.

#DEFINICION *Establecimiento -* sede o domicilio donde la empresa realiza una actividad económica.

## Identificación
Un establecimiento esta identificado por los siguientes tres factores.

**[Empresa](./Empresa):** 
	- Persona física o jurídica que posee una relación de tenencia con la instalación. 
	- Definido por el **NIF**.
- **[Instalación](./Instalaciones):** 
	- Ubícación física del establecimiento. 
	- Definido por la **referencia catastral**.
- **[Actividad](./Actividad económica):** 
	- Actividad económica realizada por la empresa en la instalación. 
	- Definido por el **código de [actividad económica](./Actividad Económica)**.

La inscripción o modificación de un establecimiento en el RIA **siempre** se iniciara a partir de la [Solicitud](./Solicitudes) de una persona física o jurídica.


El establecimiento está identificado de forma uníca por un **código RIA**.

<hr>
![fig](./_assets/information_icon.png)   **CÓDIGO RIA**

#DEFINICION *Código RIA -* código que identifica, de forma única, un establecimiento.

Formato: **PP/XXXXX**.
	- **PP** indica la provincia de la delegación grabador.
	- **XXXXX** código secuencial por provincia.

#ADVERTENCIA El código secuencial se asigna manualmente, lo que provoca huecos en la secuencia.

Este código se genera cuando se asocia por primera vez  la instalación con la empresa  y la actividad a desarrollar.

Los códigos RIA **no son reutilizables**.

![fig](./_assets/Red_question_icon.png) #PENDIENTE ¿Un cambio de actividad en un establecimiento supondría la generación de un nuevo código RIA? ¿Supondría marcar el cese de actividad para el RIA actual?

<hr>


## Tenencia
#DEFINICION *Tenencia -* Relación de titularidad entre una **[empresa agroalimentaria](./Empresas)** y una instalación en la que desarrolla, al menos,  una actividad económica.  Puede ser de **propiedad** o de **arrendamiento**. 

Una relación de tenencia de una empresa sobre una instalación puede estar vigente o haber sido finalizada.

Un establecimiento puede tener múltiples **arrendadores** y/o **propietarios** simultaneamente.

#ADVERTENCIA Un establecimiento puede tener multiples relaciones de tenencia simultaneamente con la misma empresa, incluso con la misma actividad económica.

En el modelo actual esto se permite mediante la utilización de un número de secuencia para distinguir cada una de ellas. Parece importante que el usuario sea advertido de esta circunstancia durante el proceso de mecanización.


## Actividad económica
La [actividad económica](.\Actividad Económica) de un establecimiento se define cómo  el Sector y Actividad que realiza la empresa tenedora en la instalación asociada.

Al poder existir múltiples empresas tenedoras, es posible estar realizando múltiples actividades distintas en la misma instalación.

Un establecimiento puede tener, opcionalmente, una **fecha de licencia de apertura de actividad**. 

#PENDIENTE finalizar definición establecimiento.


## Operaciones
- Alta
- Modificación
- Cambio de actividad.
- 