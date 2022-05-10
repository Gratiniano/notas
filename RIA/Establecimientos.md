# Industrias/Establecimientos
#DEFINICION *Industria -* Conjunto de instalaciones dedicadas a una actividad económica. En nuestro estarán determinadas por su relación con una  persona física ó jurídica.

#DEFINICION *Instalación -* recinto o espacio provisto de los médios necesarios para llevar a cabo una actividad económica. Estará identificado por su referencia catastral.

#DEFINICION *Establecimiento -* Cada una de las instalaciones dedicadas a la realización de una actividad economica concreta y para una empresa determinada a través de una relación de tenencia.

#DEFINICION *Tenencia -* Relación de titularidad entre una **[empresa agroalimentaria](./Empresas)** y una instalación en la que desarrolla, al menos,  una actividad económica.  Puede ser de **propiedad** o de **arrendamiento**.   

#DEFINICION *Propietario -* Una empresa, que mantiene una relación de propiedad sobre una instalación. **Esta empresa no tendría porqué ser agroalimentaria** y por tanto no está obligada a realizar ninguna actividad en la instalación.


## Establecimiento
Un establecimiento esta identificado por los siguientes tres vectores.
- **Empresa:** 
	- Persona física o jurídica que posee una relación de tenencia con la instalación. 
	- Definido por el **NIF**.
- **Instalación:** 
	- Ubícación física del establecimiento. 
	- Definido por la **referencia catastral**.
- **Actividad:** 
	- Actividad económica realizada por la empresa en la instalación. 
	- Definido por el **código de [actividad](./Actividad Económica)**.

La inscripción o modificación de un establecimiento en el RIA siempre se iniciara a partir de la [Solicitud](./Solicitudes) de una persona física o jurídica.

El establecimiento está identificado de forma uníca por un **código RIA**.

### Código RIA.
#DEFINICION *Código RIA -* código que identifica, de forma única un establecimiento.

Formato: **PP/XXXXX**.
	- **PP** indica la provincia de la delegación grabador.
	- **XXXXX** código secuencial por provincia.

#ADVERTENCIA El código secuencial se asigna manualmente, lo que provoca huecos en la secuencia.

Este código se genera cuando se asocia por primera vez  la instalación con la empresa  y la actividad a desarrollar.

![[Red_question_icon.png]] #PENDIENTE ¿Un cambio de actividad en un establecimiento supondría la generación de un nuevo código RIA? 

Los códigos RIA **no son reutilizables**.

### Tenencia
Una relación de tenencia de una empresa sobre una instalación puede estar vigente o haber sido finalizada.

Un establecimiento puede mantener simultaneamente múltiples relaciones de **arrendamiento** vigentes.

Un establecimiento sólo puede mantener una única relación de **propiedad** vigente de forma simultanea.

Un establecimiento solo puede mantener una única relación de tenencia vigente simultaneamente con la misma empresa.
![[Red_question_icon.png]] #PENDIENTE ¿Un establecimiento puede tene multiples relaciones de arrendamiento simultaneamente con la misma empresa si cada una de ellas corresponde a una actividad económica distinta? ¿Es esto relevante?





#PENDIENTE finalizar definición establecimiento.