---
title:   Desarrollo Guiado por Pruebas
isChild: true
anchor:  test_driven_development
---

## Desarrollo Guiado por Pruebas {#test_driven_development_title}

De [Wikipedia](https://wikipedia.org/wiki/Test-driven_development):

> El desarrollo dirigido por pruebas (TDD, por sus siglas en inglés) es un proceso de desarrollo de software que se basa
> en la repetición de un ciclo de desarrollo muy corto: primero, el desarrollador escribe un caso de prueba automatizado que falla
> y que define una mejora deseada o una nueva función; después, produce código para superar esa prueba y,
> por último, refactoriza el nuevo código para que cumpla unos estándares aceptables. Kent Beck, a quien se atribuye haber
> desarrollado o "redescubierto" la técnica, declaró en 2003 que el TDD fomenta los diseños sencillos e inspira confianza.

Hay varios tipos diferentes de pruebas que puede realizar para su aplicación:

### Pruebas Unitarios

Las pruebas unitarias son un enfoque de programación para garantizar que las funciones, clases y métodos funcionan como se espera,
desde el momento en que se construyen hasta el final del ciclo de desarrollo. Comprobando los valores que entran y salen de varias
funciones y métodos, puedes asegurarte de que la lógica interna funciona correctamente. Mediante el uso de la inyección de dependencias
y la creación de clases y stubs "simulados", puede comprobar que las dependencias se utilizan correctamente para mejorar aún más la cobertura de las pruebas.

Cuando creas una clase o función deberías crear una prueba unitaria para cada comportamiento que deba tener. A un nivel muy básico
deberías asegurarte de que da error si le envías argumentos erróneos y asegurarte de que funciona si le envías argumentos válidos.
Esto ayudará a asegurar que cuando hagas cambios a esta clase o función más adelante en el ciclo de desarrollo, la funcionalidad antigua
siga funcionando como se esperaba. La única alternativa a esto sería `var_dump()` en un test.php, que no es forma de construir
una aplicación - grande o pequeña.

La otra utilidad de las pruebas unitarias es contribuir al código abierto. Si puedes escribir una prueba que muestre una
funcionalidad rota (es decir, que falla), luego arreglarla, y mostrar que la prueba pasa, es mucho más probable que los parches sean aceptados.
Si diriges un proyecto que acepta pull requests, deberías sugerirlo como requisito.

[PHPUnit](https://phpunit.de/) PHPUnit es el marco de pruebas de facto para escribir pruebas unitarias para aplicaciones PHP,
pero existen varias alternativas:

* [atoum](https://github.com/atoum/atoum)
* [Kahlan](https://github.com/kahlan/kahlan)
* [Peridot](https://peridot-php.github.io/)
* [Pest](https://pestphp.com/)
* [SimpleTest](https://github.com/simpletest/simpletest)

### Pruebas de Integración

De [Wikipedia](https://wikipedia.org/wiki/Integration_testing):

Las pruebas de integración (a veces denominadas integración y pruebas, abreviadas "I&T") son la fase de las pruebas de software
en la que se combinan módulos de software individuales y se prueban como un grupo. Se realiza después de las pruebas unitarias
y antes de las de validación. Las pruebas de integración toman como entrada los módulos que se han probado por unidades,
los agrupan en conjuntos más grandes, aplican a esos conjuntos las pruebas definidas en un plan de pruebas de integración
y entregan como salida el sistema integrado listo para las pruebas del sistema.

Muchas de las mismas herramientas que pueden utilizarse para las pruebas unitarias pueden emplearse para las pruebas de integración,
ya que se utilizan muchos de los mismos principios.

### Pruebas Funcionales

A veces también conocidas como pruebas de aceptación, las pruebas funcionales consisten en utilizar herramientas para crear pruebas
automatizadas que realmente utilizan la aplicación, en lugar de limitarse a verificar que las unidades individuales de código se comportan
correctamente y que las unidades individuales pueden hablar entre sí correctamente.
Estas herramientas suelen funcionar utilizando datos reales y simulando usuarios reales de la aplicación.

#### Herramientas de Pruebas Funcionales

* [Selenium](https://www.selenium.dev/)
* [Mink](https://mink.behat.org/)
* [Codeception](https://codeception.com/) es un marco de pruebas de pila completa que incluye herramientas de pruebas de aceptación
* [Storyplayer](https://github.com/MeltwaterArchive/storyplayer) es un marco de pruebas completo que permite crear y destruir entornos de prueba a petición del usuario.
