
#FEATURE La provincia, el municipio y la localidad deben existir y ser consistentes.
```Gherkin
#language:es

Caracteristica: la provincia, municipio y localidad deben ser consistentes entre si.

Antecedentes: 

	# Este característica es trasversal y puede ser utilizada en varias pantallas
	
	Dado que estamos la pantalla de edición de "entidad".

Regla: Los datos de provincia, municipio y localidad deben ser consistentes entre si.

	@API_REST
	Escenario: la provincia el municipio y la localidad son consistentes
			
		Cuando introducimos los datos de <provincia>, <municipio> y <localidad>
		Entonces se muestra el siguiente <mensaje>
			Y la posibilidad de guardar los cambios queda en <estado>
			
		Ejemplos:
		| descripcion | provincia | municipio          | localidad     | mensaje                         | estado      |
		| ----------- | --------- | ------------------ | ------------- | ------------------------------- | ----------- |
		| Happy path  | ALBACETE  | CASAS DE DON PEDRO | EL JARDIN     |                                 | SIN CAMBIO  |
		| Error Prov. | WYOMING   | <indiferente>      | <indiferente> | La provincia indicada no existe | DESACTIVADO |	
		| Error Muni. | ALAVA     | VILLARROBLEDO      | <indiferente> | El municipio indicado no existe | DESACTIVADO |	
		| Error Loca. | ALBACETE  | CASAS DE DON PEDRO | VILLARROBLEDO | La localidad indicada no existe | DESACTIVADO |

	@UI_Test
	Escenario: la provincia y el municipio son consistentes en el formulario 

		# SUPONEMOS QUE la selección de municipios siempre se producirá sobre listas de opciones cerradas.
		
		Dado que hemos seleccioado la provincia <provincia>
		Cuando queremos seleccionar un municipio
		Entonces en la lista de municipios pueden aparecer <municipios_ok>
			Pero no pueden aparecer <municipios_fail>
						
		Ejemplos:
		| descripcion | provincia | municipios_ok              | municipios_fail            |
		| ----------- | --------- | -------------------------- | -------------------------- |
		| happy path  | ALBACETE  | ALBACETE, ALATOZ, BACARIZA | VITORIA, BILBAO, LANTARON  |
		| happy path2 | ALAVA     | VITORIA, BILBAO, LANTARON  | ALBACETE, ALATOZ, BACARIZA |


	@UI_Test
	Escenario: la provincia, municipio y localidad son consistentes en el formulario 

		# SUPONEMOS QUE la seleccion de provincia, municipio y localidad siempre se produce sobre listas de opciones cerradas.
		# SUPONEMOS que la selección de provincia municipio ya se ha realizado.
		Dado que hemos seleccionado la provincia <provincia>
			Y hemos seleccionado el municipio <municipio>
		Cuando queremos seleccionar una localidad
		Entonces en la lista de localidades aparecen las localidades <localidad_OK>
			Pero no pueden aparecer <municipios_FAIL>
						
		Ejemplos:
		| descripcion | provincia | municipio | localidad_OK                                       | localidad_FAIL                |
		| ----------- | --------- | --------- | -------------------------------------------------- | ----------------------------- |
		| happy path  | ALBACETE  | ALPERA    | ALPERA, CASAS DE DON PEDRO, LAS FUENTES, LA LAGUNA | ALCARAZ, CANALEJA, EL HORCAJO |
		| happy path2 | ALBACETE  | AYNA      | AYNA                                               | ALPERA, ALCARAZ, ALBACETE     |



Regla: Cuando no se introduce la localidad se toma la localidad por defecto

	# Los municipios compuestos por más de una localidad siempre toman una localidad por defecto indicada por el
	# código de localidad cero (0).
	# Los municipios compuestos por una única localidad siempre toman cómo código de localidad el cero (0)

	@API_REST
	Escenario: seleccion de localidad por defecto
		Cuando introducimos los datos de <provincia>, <municipio> y <localidad>
		Entonces se establece como localidad <resultado>
			
		Ejemplos:
		| descripcion  | provincia | municipio          | localidad | resultado          |
		| ------------ | --------- | ------------------ | --------- | ------------------ |
		| por defecto  | ALBACETE  | CASAS DE DON PEDRO |           | CASAS DE DON PEDRO |			
		| contrajemplo | ALBACETE  | CASAS DE DON PEDRO | EL JARDIN | EL JARDIN          |



	@UI_Test
	Escenario: seleccion de localidad por defecto con unica localidad 
		# SUPONEMOS QUE la seleccion de provincia, municipio y localidad siempre se produce sobre listas de opciones cerradas.
		# Si hay más de una localidad no seleccionamos ninguna
		# Si hay una única localidad la seleccionamos por defecto, en otro caso la dejamos pendiente de selecciona
		Dado que hemos seleccionado la provincia <provincia>
			Y hemos seleccionado el municipio <municipio>
		Cuando  existe(n) <localidad_count> localidad(es) ese municipio y provincia
		Entonces se establece como localidad <localidad_default>

	Ejemplos:
	| descripcion | provincia | municipio | localidad_OK                                       | localidad_FAIL | contador | localidad_default |
	| ----------- | --------- | --------- | -------------------------------------------------- | -------------- | -------- | ----------------- |
	| happy path  | ALBACETE  | ALPERA    | ALPERA, CASAS DE DON PEDRO, LAS FUENTES, LA LAGUNA | ALCARAZ        | 4        |                  |
	| happy path2 | ALBACETE  | AYNA      | AYNA                                               | ALPERA         | 1        | AYNA              |

	
```
