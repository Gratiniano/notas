# Empresas

#DEFINICION *Empresa -* Persona física o jurídica identificada por un NIF.

<hr>
![fig](../_assets/Information_icon.png)  **REGISTRO DE TERCEROS** 

#DEFINICION *Registro de Terceros -* Repositorio donde se centraliza la información de personas físicas o jurídicas relevantes para la gestión de la Consejería.
 
Las empresas, junto a su información de contacto, deberían estár registradas en el **registro de terceros**.

Idealmente, el registro de una empresa en RIA provocaría la inclusión de dicha empresa en el **registro de terceros**.

La baja de una empresa en RIA, **no necesariamente** provocará la baja de esa misma empresa en el registro de terceros.

<hr>


## Una empresa no es una industria
* Una empresa no posee un código RIA.
* Una empresa no desempeña un único tipo de actividad.
* Una empresa no admite ampliaciones ni mejoras.
* Una empresa siempre está asociada a un NIF.
* Una empresa aporta datos de contacto.
* Una empresa puede tener un representante que, a su vez, debería ser incluido en el **registro de terceros**.
* La **sede** o **domicilio** particular donde la empresa realiza una actividad económica es el  [Establecimiento](Establecimientos)


## Representante
#DEFINICION cualquier persona física o jurídica que actue en representación del o los propietarios de la empresa. Es una figura **opcional** en RIA.

Todas las comunicaciones a la empresa deberán hacerse a través del representante.

Deberá aportar información información de contacto incluyendo:
- Cargo que desempeña en la empresa.
- Dirección Postal.
- Dirección electrónica.



## Alta de empresa
Una empresa puede ser incluida en el sistema debido a:
	- una [Solicitud de inscripción](../Solicitudes) presentada por una persona no existente en RIA.	
	- de oficio, por parte de la Administración.

![fig](../_assets/Red_question_icon.png) #PENDIENTE ¿En qué casos puede darse de alta de oficio una empresa?

#ADVERTENCIA  el alta de una empresa en RIA siempre debería estar asociado al alta de un Establecimiento.


## Modificacion de empresa #PENDIENTE 

Las modificaciones de datos de una empresa solo pueden hacerse sobre:
- Su información de contacto.
- Información del representante.

## Baja de empresa
Podemos distinguir dos casos

### Borrado lógico.
Una empresa puede ser dada de baja en estos dos casos:
	- Cuando haya sido dada de alta de oficio y no tenga establecimientos asociados.
	- Cuando el solicitante haya indicado el desistimiento de la inscripción

Las empresas con borrado lógico no aparecerá en listados ni informes.

#PENDIENTE Explorar las implicaciones que puede tener una baja lógica de empresa.
#PENDIENTE #ADVERTENCIA  Aclarar las condiciones de desistimiento.

### Cese de actividad
Se puede establecer que una empresa ha cesado su actividad cuando:
	- El solicitante original ha solicitado su baja en el RIA mediante una [Solicitud](../Solicitudes).
 
El cese de actividad se transmitirá en cascada a todas las relaciones de tenencia con establecimiento que la empresa tenga activas.


## Features
#FEATURE Alta de una empresa en RIA.
```Gherkin
#language:es

Característica: los usuarios pueden registrar nuevas empresas en RIA.

	# Esta característica depende de la característica validacion_consistencia_localidad
	# (../shared/validacion_consistencia_localidad.feature).


Antecedentes: 
	Dado que nos encontramos en la pantalla de creación de empresas
	  Y en el repositorio ya existen las empresas
		  | nif       | nombre   | fecha alta | activa | borrada |
		  | 52761552N | ALOZANO  | 01/01/2020 | S      | N |
		  | G16034662 | PSANCHEZ | 01/01/2020 | N      | S |
		  | B16108045 | MROBLES  | 01/02/2020 | N      | N |
		Y que la fecha actual es '31/12/2021'
		Y se han introducido, al menos, los datos mínimos de empresa
		
Regla: las empresas que no han existido nunca se inscriben en RIA.

	Escenario: Registrar una empresa nueva
		Dado que queremos registrar una empresa con los siguientes datos 
			| nif       | nombre   | 
			| F16037228 | FCASADO  | 
				
		Entonces en el erpositorio debería aparecer la siguiente empresa
			| nif       | nombre   | fecha alta | activa | borrada |
			| F16037228 | FCASADO  | 31/12/2021 | S      | N |


Regla: los datos de empresas borradas se reescriben

	Escenario: Registrar una nueva empresa que fue borrada en el pasado
		Dado que queremos registrar una empresa con los siguientes datos 
			| nif       | nombre   | 
			| G16034662 | AMOLINA  | 
				
		Entonces en el repositorio debería aparecer la siguiente empresa
			| nif       | nombre   | fecha alta | activa | borrada |
			| G16034662 | AMOLINA  | 31/12/2021 | S      | N |


Regla: los datos de las empresas en fin de actividad se reescriben.

	Escenario: Registrar una nueva empresa que cuyo CIF fue marcado en fin de actividad.
		Dado que queremos registrar una empresa con los siguientes datos 
			| nif       | nombre   | 
			| B16108045 | VALONSO  | 
				
		Entonces en el repositorio debería aparecer la siguiente empresa
			| nif       | nombre   | fecha alta | fecha modif |activa | borrada |
			| B16108045 | VALONSO  | 01/01/2020 | 31/12/2021  |  S    | N |		



Regla: No se puede volver a registrar una empresa que está activa.

	Escenario: Registrar una nueva empresa que cuyo CIF fue marcado en fin de actividad.
		Dado que queremos registrar una empresa con los siguientes datos 
			| nif       | nombre   | 
			| 52761552N | RALONSO  | 
				
		Entonces se muestra un mensaje informativo al usuario
			Y en el repositorio debería aparecer la siguiente empresa
			| nif       | nombre   | fecha alta | activa | borrada |
			| 52761552N | ALOZANO  | 01/01/2020 | S      | N |


```

#FEATURE Modificación de una empresa en RIA
```Gherkin
#language:es

Caracteristica: modificación de datos de una empresa


	# Esta característica depende de la característica validacion_consistencia_localidad
	# (../shared/validacion_consistencia_localidad.feature).

Antecedentes: 
	Dado que estamos en la pantalla de modificación de empresa
		Y en el repositorio existen las empresas  
		  | nif       | nombre     | prov | muni | loc | cod post | direccion      | F.Jur | F.Datos    | Cese | Borrado |  
		  | G16034662 | ALOZANO    | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 01/01/2020 | N    | N       |  
		  | 52761552N | BLEONES    | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 01/01/2020 | S    | N       |  
		  | B16108045 | RECAVIN    | 16  | 249  | 0    | 16415    | C/LIMON 5      | 9     | 01/01/2020 | N    | S       |  
		Y la fecha en curso es '31/12/2021'
		Y se han introducido, al menos, los datos mínimos de empresa



Regla: la modificación de los datos de una empresa actualiza los datos y la cronología pero no el estado.

	Esquema del escenario: Todos los datos empleados son válidos 
		Cuando queremos modificar los siguientes datos de empresas en RIA
		 | nif          | nombre     | prov | muni | loc  | cod post | direccion      | F.Jur |  
		 | G16034662    | MNIETO     | 2    | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 
		 | 52761552N    | BLEONES    | 16   | 78   | 9    | 02600    | C/VIRGEN, 23   | 9     | 
		 
		Entonces en el repositorio deberían aparecer las siguientes empresas
		  | nif          | nombre     | prov | muni | loc | cod post | direccion      | F.Jur | F.Datos    | Cese | Borrado |  
		  | G16034662    | MNIETO     | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 01/01/2020 | N    | N       |  
		  | 52761552N    | BLEONES    | 16  | 78   | 9    | 02600    | C/VIRGEN, 23   | 9     | 01/01/2020 | S    | N       |  
		


```

#FEATURE Baja de una empresa. Borrado lógico
#PENDIENTE Baja de una empresa. Borrado lógico. Revisar ejemplos.
```Gherkin
#language:es

Característica: Baja de una empresa. Borrado lógico.

# Las empresas que están en borrado lógico no aparecen en listados o informes. A todos los efectos no han sido registradas en RIA.

Regla: se pueden dar de baja empresas creadas de oficio sin establecimientos.


	Esquema del escenario: dar de baja una empresa creada de oficio 
		Dado que la empresa <nif> fue creada <tipo_creacion>
			Y la fecha actual es '31/12/2022'
			Y tiene <nro_establs> establecimiento(s) asociado(s)
		Cuando indicamos que se le dé de baja
		Entonces el sistema nos muestra el mensaje <mensaje>
			Y en el repositorio se le asigna la  fecha de baja <f_baja>

		Ejemplos: 
		| nif       | nombre  | tipo_creacion | nro_establs | f_baja   | mensaje                                                       |
		|-----------|---------|---------------|-------------|----------|---------------------------------------------------------------|
		| G16034662 | MNIETO  | DE OFICIO     | 0           | 31/12/21 | Empresa eliminada                                             |
		| 52761552N | BLEONES | DE OFICIO     | 1           |          | No se puede eliminar una empresa con establecimientos activos |

		
Regla: se pueden dar de baja empresas por desistimiento del solicitante.

	Esquema del escenario: dar de baja empresa por desistimiento
		Dado que la empresa <nif> fue creada <tipo_creacion>
			Y el solicitante ha manifestado su intención de desistir en la inscripción con fecha <f_solicitada>
			Y <cumple_desistimiento> cumple las condiciones de desistimiento
		Cuando indicamos que se le de de baja
		Entonces el sistema nos muestra el siguiente mensaje <mensaje>
			Y en el repositorio se le asigna como fecha de baja <f_baja>
			Y al establecimiento(s) asociado(s) <establs> se les asigna la fecha de baja <f_baja>

		Ejemplos:
		| nif       | nombre  | tipo_creacion | cumple_desistimiento | f_solicitada | establs  | f_baja   | mensaje                                                         |
		| --------- | ------- | ------------- | -------------------- | ------------ | -------- | -------- | --------------------------------------------------------------- |
		| G16034662 | MNIETO  | POR SOLICITUD | CUMPLE               | 15/12/2021   | 16/00015 | 31/12/21 | Se ha cancelado la inscripción de la empresa en RIA.            | 
		| 52761552N | BLEONES | POR SOLICITUD | NO CUMPLE            | 15/12/2021   | 02/01012 |          | La inscripción de la empresa es firme y no puede ser desistida. |

	
```

#FEATURE  Baja de una empresa. Cese de actividad.
#PENDIENTE Baja de una empresa. Cese de actividad. Revisar ejemplos.
```Gherkin
#language:es

Característica: Baja de una empresa. Cese de actividad.

# Las empresas cuya activida cesa siguen siendo accesibles por la aplicación.

Regla: El cese de actividad de una empresa en RIA supone, además,  el fin de sus relaciones con establecimientos.

	Esquema del escenario: Registrar el cese de actividad de una empresa 
		Dado que la empresa <nif> o su representante <nif_rep> han presentado una solicitud de cese de actividad con fecha <f_solicitada>
			Y tiene <establs> establecimiento(s) asociado(s)
		Cuando indicamos que se le dé de baja
		Entonces el sistema  muestra el mensaje <mensaje>
			Y en el repositorio se le asigna como fecha de cese de actividad <f_cese>
			Y al establecimiento(s) asociado(s) <establs> se les asigna la fecha de cese de actividad <f_cese>
		Ejemplos:
		| nif       | nif_rep | nombre  | f_solicitada | f_cese   | establs  | f_cese_estab | mensaje                                                                        |
		|-----------|---------|---------|--------------|----------|----------|--------------|--------------------------------------------------------------------------------|
		| 52761552N |         | BLEONES | 31/12/2021   | 31/12/21 | 16/00015 | 31/12/21     | Registrado el fin de actividad de la empresa y sus establecimientos asociados. |
		| G16034662 |         | MNIETO  | 31/12/2021   |          |          |              | Registrado el fin de actividad de la empresa.                                  |
		

```
