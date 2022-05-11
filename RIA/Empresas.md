# Empresas

#DEFINICION *Empresa -* Persona física o jurídica identificada por un NIF.

<hr>
![fig](./_assets/Information_icon.png)  **REGISTRO DE TERCEROS** 

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

![fig](./_assets/red_question_icon.png) #PENDIENTE ¿En qué circunstancias puede darse de alta de oficio una empresa?

#ADVERTENCIA  el alta de una empresa en RIA siempre debería estar asociado al alta de un Establecimiento.


## Features
#FEATURE Alta de una empresa en RIA.
```Gherkin
#language:es

Característica: los usuarios pueden registrar nuevas empresas en RIA.

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
#language=es

Caracteristica: modificación de datos de una empresa

Antecedentes: 
	Dado que estamos en la pantalla de modificación de empresa
		Y en el repositorio existen las empresas  
		  | nif          | nombre     | prov | muni | loc | cod post | direccion      | F.Jur | F.Datos    | Cese | Borrado |  
		  | G16034662    | ALOZANO    | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 01/01/2020 | N    | N       |  
		  | 52761552N    | BLEONES    | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 01/01/2020 | S    | N       |  
		  | B16108045    | RECAVIN    | 16  | 249  | 0    | 16415    | C/LIMON 5      | 9     | 01/01/2020 | N    | S       |  
		Y la fecha en curso es '31/12/2021'
		Y se han introducido, al menos, los datos mínimos de empresa



Regla: la modificación de los datos de una empresa actualiza la cronología pero no el estado.

	Escenario: Todos los datos empleados son válidos 
	Cuando queremos modificar los siguientes datos de empresas en RIA
	 | nif          | nombre     | prov | muni | loc | cod post | direccion      | F.Jur |  
	 | G16034662    | FSANCHO    | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 
	 | 52761552N    | BLEONES    | 2   | 81   | 0    | 02600    | C/MAYOR 1      | 9     | 
	 | B16108045    | RECAVIN    | 16  | 249  | 0    | 16415    | C/LIMON 5      | 9     | 	 
	
	Entonces <postcondicion>
		Y <postcondicion>
	
```