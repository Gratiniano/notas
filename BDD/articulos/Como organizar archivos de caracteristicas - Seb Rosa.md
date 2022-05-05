# ¿Cómo organizar archivos de características?
Seb Rosa -2021. https://cucumber.io/blog/bdd/solving-how-to-organise-feature-files/

## Encuesta usuarios
En 2021 Specflow realizó una [encuesta](https://specflow.org/challenges/organise-feature-files/) entre usuarios sobre la forma de organizar features con el siguiente resultado:
![fig1](https://static1.smartbear.co/cucumber/media/images/blog/gwt-barchart.png)

`Ejemplo. Dividir por area funcional, agrupar por capacidad`
```text
features/
  payments/
    cards/
      mastercard-processing.feature
      visa-processing.feature
  reports/
    account/
      personal-account-report.feature
      company-account-report.feature
```



La motivación principal aportada por los participantes es:

 "*El software que se desarrolla es para fines comerciales, por lo tanto, la capacidad de dominar la capacidad comercial es primordial sobre el aspecto técnico. 
 
 Me gusta la idea de poder precisar rápidamente los componentes del sistema que generan problemas, por lo que una estructura de soporte que transmita qué componente del sistema tiene la "culpa" es muy bienvenida. 
 
 Por lo general, hago esto con etiquetas y evalúo la prueba. 
 
 Informes basados en etiquetas…*"


## ¿Especificación o prueba?
Motivaciones de BDD:

    - Especificación del comportamiento del sistema.
    - Automatización de las pruebas.

La opcion ganadora del desafio apunta a que Gherkin se utiliza para especificar el comportamiento del sistema. Indican que se espera que los archivos de funciones se utilicen como documentación viva.
Esto coincide con la orientación de *BDD* y *SBE*.

## Las características son documentación 

**PROBLEMA:** ¿Qué es exactamente una función?

### Navegando por la documentación
Un arbol jerárquico de carpetas es una forma simple de organizar la información (similar a la tabla de contenidos o índice de un libro).

`Ejemplo: entrega de pizzas on-line.

![fig2](https://static1.smartbear.co/cucumber/media/images/blog/gwt-fig2.png)

### Acercar/Alejar
El nivel de detalle deseado se consigue mediante la anidación de las carpetas.
![fig3](https://cucumber.io/cucumber/media/images/blog/gwt-fig3.png)



### Especificación de comportamientos compartidos
Ejemplo: funcion send_email.feature.
Su comportamiento debe describirse en un único archivo de funciones.
![fig4](https://cucumber.io/cucumber/media/images/blog/gwt-fig4.png)


<hr>
**Como compartir funciones entre escenarios**

Gherkin no proporciona un mecanismo de referencia.
La única opción es documentarlo en el escenario incluyendo el nombre y ruta relativa del archivo.

```Gherkin
Feature: enviar enlace único.

  Esta función depende de:
  - Enviar correo electrónico - ../../../communication/email/send_email.feature
    
```
<hr>

### Documentación dirigida
Diferentes consumidores requieren información diferente (clientes, desarrolladores, testers, etc.).

#### Opcion 1: jerarquias separadas para partes interesadas.
![fig5](https://cucumber.io/cucumber/media/images/blog/gwt-fig5.png)

### Opcion 2: Intercalar la documentación específica.
![fig6](https://cucumber.io/cucumber/media/images/blog/gwt-fig5.png)

<hr>

**Etiquetas**

Cuando no es práctico representar jerárquicamente los intereses transversales se pueden usar las [etiquetas](https://cucumber.io/docs/cucumber/api/#tags).

<hr>

## Las historias no son características (features).
Las historias se utilizan para ofrecer pequeños incrementos de funcionalidad. Los archivos de funciones asociados a historias solo describen una pequeña parte de la funcionalidad.
