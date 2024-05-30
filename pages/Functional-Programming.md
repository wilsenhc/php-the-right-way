---
layout: page
title:  Functional Programming in PHP
sitemap: true
---

# Programación Funcional en PHP

PHP supports first-class functions, meaning that a function can be assigned to a variable. Both user-defined and
built-in functions can be referenced by a variable and invoked dynamically. Functions can be passed as arguments to
other functions and a function can return other functions (a feature called higher-order functions).

Recursion, a feature that allows a function to call itself, is supported by the language, but most of the PHP code
focus is on iteration.

Anonymous functions (with support for closures) have been present since PHP 5.3 (2009).

PHP 5.4 agregó la capacidad de unir `closures` al ámbito de un objeto mejorando el soporte a las llamadas de tal manera que puedan ser intercambiables con funciones anónimas en casi todos los casos.

The most common usage of higher-order functions is when implementing a strategy pattern. The built-in `array_filter()`
function asks both for the input array (data) and a function (a strategy or a callback) used as a filter function on
each array item.

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

A closure is an anonymous function that can access variables imported from the outside scope without using any global
variables. Theoretically, a closure is a function with some arguments closed (e.g. fixed) by the environment when it is
defined. Closures can work around variable scope restrictions in a clean way.

In the next example we use closures to define a function returning a single filter function for `array_filter()`, out
of a family of filter functions.

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

Each filter function in the family accepts only elements greater than some minimum value. The single filter returned by
`criteria_greater_than` is a closure with `$min` argument closed by the value in the scope (given as an argument when
`criteria_greater_than` is called).

Early binding is used by default for importing `$min` variable into the created function. For true closures with late
binding one should use a reference when importing. Imagine a templating or input validation library, where a closure is
defined to capture variables in scope and access them later when the anonymous function is evaluated.

* [Read about Anonymous functions][anonymous-functions]
* [More details in the Closures RFC][closures-rfc]
* [Read about dynamically invoking functions with `call_user_func_array()`][call-user-func-array]


[anonymous-functions]: https://www.php.net/functions.anonymous
[closures-rfc]: https://wiki.php.net/rfc/closures
[call-user-func-array]: https://www.php.net/function.call-user-func-array
