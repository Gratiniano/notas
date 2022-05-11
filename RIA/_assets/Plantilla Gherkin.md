```Gherkin
#language:es

Caracteristica: <nombre de la feature>

Antecedentes: <background comun a todos los casos>
	Dado que <precondicion>

Regla: <regla de negocio que se pretende ilustrar>

	Escenario: <nombre del escenario>
	Dado que <precondicion>
	 Y <precondicion>
	Cuando <evento disparador de la transición>
	Entonces <postcondicion>
		Y <postcondicion>
	
```