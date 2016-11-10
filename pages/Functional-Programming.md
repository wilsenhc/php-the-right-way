---
layout: page
title: Programación Funcional en PHP
---

# Programación Funcional en PHP

PHP soporta funciones de primera-clase, lo que significa que una función puede asignarse a una variable. De igual forma, tanto las funciones definidas por el usuario como las funciones nativas de PHP pueden ser referenciadas por una variable e invocarse dinámicamente. Las funciones pueden ser pasadas como argumentos / parámetros a otras funciones (funciones de orden superior) y una función puede retornar otras funciones.

La recursión, una característica que permite a una función llamarse a sí misma, es soportada por el lenguaje, sin embargo, PHP se enfoca en la iteración.

Las nuevas funciones anónimas (con soporte para `closures`) están presentes a partir de PHP 5.3 (2009).

PHP 5.4 agregó la capacidad de unir `closures` al ámbito de un objeto mejorando el soporte a las llamadas de tal manera que puedan ser intercambiables con funciones anónimas en casi todos los casos.

El uso más común para las funciones de orden superior es cuando se implementa un patrón estrategia. La función interna `array_filter` solicita dos argumentos, una matriz (data) y una función de retorno (callback) o patrón estrategia que se usará como filtro para cada elemento de la matriz.

{% highlight php %}
<?php
$entrada = array(1, 2, 3, 4, 5, 6);

// Crea una nueva función anónima y la asigna a una variable
$filtro_inclusivo = function($elemento) {
    return(($elemento % 2) == 0);
};

// La función interna array_filter acepta ambos, data y la función
$retorno = array_filter($entrada, $filtro_inclusivo);

// La función NO necesita ser asignada a una variable. Esto es válido también:
$retorno = array_filter($entrada, function($elemento) {
    return(($elemento % 2) == 0)
});

print_r($retorno);
{% endhighlight %}

Un `closure` es una función anónima que puede acceder a las variables importadas fuera del ámbito sin usar variables globales. En teoría, un `closure` es una función con algunos argumentos cerrados (por ejemplo, fijo) por el entorno cuando este ha sido definido. Los `closures` pueden evitar las restricciones de ámbito de variables de una manera limpia.

En el siguiente ejemplo usaremos `closures` para definir una función que retorne una función de filtro sencilla para `array_filter`, fuera de una familia de funciones de filtro.

{% highlight php %}
<?php
/**
 * Se crear un una función anónima de filtrado que aceptará elementos > $min
 *
 * Retorna un filtro sencillo fue de la familia de de filtros "mayores que n"
 */
function criterio_mayor_que($min)
{
    return function($elemento) use ($min) {
        return $elemento > $min;
    };
}

$entrada = array(1, 2, 3, 4, 5, 6);

// Use array_filter sobre una entrada con una función de filtro seleccionada
$salida = array_filter($entrada, criterio_mayor_que(3));

print_r($salida); // elementos > 3
{% endhighlight %}

Cada función de filtro en la familia aceptará sólo los elementos mayores que el valor mínimo. El filtro sencillo retornado por `criterio_mayor_que` es un `closure` con un argumento `$min` cerrado por el valor en el ámbito (dado como argumento cuando `criterio_mayor_que` es llamado).

El primer enlace es usado por defecto para importar la variable `$min` en la función. Para `closures` verdaderos con uniones tardías debe usarse una referencia cuando se importen. Imagina una plantilla o bibliotecas de validación de entradas, donde se define el `closure` para capturar variables en el ámbito y acceder luego, cuando se evalúe la función anónima.

* [Leer acerca de Funciones Anónimas][anonymous-functions]
* [Más detalles en el RFC de Closures][closures-rfc]
* [Leer acerca de la invocación dinámica de funciones con `call_user_func_array`][call-user-func-array]

[anonymous-functions]: http://www.php.net/manual/en/functions.anonymous.php
[call-user-func-array]: http://php.net/manual/en/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures
