---
title:   Paradigmas de Programación
isChild: true
anchor:  paradigmas_de_programacion
---

## Paradigmas de Programación {#paradigmas_de_programacion_title}

PHP es un lenguaje flexible y dinámico que admite diversas técnicas de programación. A lo largo de los años ha evolucionado de forma espectacular,
sobre todo con la incorporación de un sólido modelo orientado a objetos en PHP 5.0 (2004), funciones anónimas
y namespaces en PHP 5.3 (2009) y traits en PHP 5.4 (2012).

### Programación orientada a Objetos

PHP tiene un conjunto muy completo de características de programación orientada a objetos, incluyendo soporte para clases,
clases abstractas, interfaces, herencia, constructores, clonación, excepciones y más.

* [Leer más sobre PHP Orientado a Objetos][oop]
* [Leer más sobre Traits][traits]

### Programación Funcional

PHP soporta funciones de primera clase, lo que significa que una función puede ser asignada a una variable. Tanto las funciones
definidas por el usuario como las funciones internas pueden referenciarse mediante una variable e invocarse dinámicamente. Las funciones pueden pasarse como argumentos a otras funciones (característica denominada _Funciones de orden superior_) y las funciones pueden devolver otras funciones.

La recursión, una característica que permite a una función llamarse a sí misma, está soportada por el lenguaje,
pero la mayor parte del código PHP se centra en la iteración.

Las nuevas funciones anónimas (con soporte para closures) están presentes desde PHP 5.3 (2009).

PHP 5.4 añadió la capacidad de enlazar closures al ámbito de un objeto y también mejoró el soporte para callables de tal forma que pueden ser usadas indistintamente con funciones anónimas en casi todos los casos.

* Continúa leyendo en [Programación Funcional en PHP](/pages/Functional-Programming.html)
* [Leer más acerca de las Funciones Anónimas][anonymous-functions]
* [Leer más sobre la clase Closure][closure-class]
* [Más detalles en el RFC Closures][closures-rfc]
* [Leer más sobre Callables][callables]
* [Más información sobre la invocación dinámica de funciones con `call_user_func_array()`.][call-user-func-array]

### Meta Programación

PHP soporta varias formas de meta-programación a través de mecanismos como la API Reflection y los Métodos Mágicos.
Hay muchos Métodos Mágicos disponibles tales como `__get()`, `__set()`, `__clone()`, `__toString()`, `__invoke()`, etc.
que permiten a los desarrolladores conectarse al comportamiento de las clases. Los desarrolladores de Ruby a menudo dicen que PHP carece de `method_missing`,
pero esto esta disponible como `__call()` y `__callStatic()`.

* [Leer más sobre métodos mágicos][magic-methods]
* [Leer más sobre Reflection][reflection]
* [Leer más sobre Sobrecarga][overloading]


[oop]: https://www.php.net/language.oop5
[traits]: https://www.php.net/language.oop5.traits
[anonymous-functions]: https://www.php.net/functions.anonymous
[closure-class]: https://www.php.net/class.closure
[closures-rfc]: https://wiki.php.net/rfc/closures
[callables]: https://www.php.net/language.types.callable
[call-user-func-array]: https://www.php.net/function.call-user-func-array
[magic-methods]: https://www.php.net/language.oop5.magic
[reflection]: https://www.php.net/intro.reflection
[overloading]: https://www.php.net/language.oop5.overloading
