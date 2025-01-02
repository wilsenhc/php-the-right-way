---
title:   Fecha y Hora
isChild: true
anchor:  fecha_y_hora
---

## Fecha y Hora {#fecha_y_hora_title}

PHP posee una clase llamada DateTime para ayudar en la lectura, escritura, comparación y el cálculo de fechas y tiempo. En PHP
aparte de DateTime existen muchas funciones relacionadas con fecha y tiempo, sin embargo, DateTime, provee una interfaz orientada a
objeto muy útil la cual se adapta a la mayoría de los casos. Adicional a eso, DateTime permite el manejo de zonas horarias, pero eso
está fuera del alcance de esta breve introducción.

Es posible realizar cálculos con DateTime gracias a la clase DateInterval. DateTime posee métodos como `add()` and `sub()` que
utilizan DateInterval como argumento. No se debe escribir codigo que espere la misma cantidad de segundo en cada día. Tanto el
horario de verano (daylight savings time) como las distintas zonas horarias invalidan esa suposición. En vez de eso, utilice
los intervalos de fechas para hacer sus cálculos. Para calcular la diferencia entre fechas utilice el método `diff()`.
Este devolverá un `new DateInterval`, el cual puede ser fácilmente impreso en la pantalla.


{% highlight php %}
<?php
$string = '22. 11. 1968';
$inicio = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Fecha inicial: ' . $start->format('Y-m-d') . PHP_EOL;
{% endhighlight %}

Es posible realizar calculos con DateTime gracias a la clase DateInterval. DateTime posee metodos como `add()` and `sub()` que
utilizan DateInterval como argumento. No se debe escribir codigo que espere la misma cantidad de segundo en cada dia. Tanto el
horario de verano (daylight savings time) como las distintas zonas horarias invalidaran esa suposicion. En vez de eso, utilice
los intervalos de fechas para hacer sus calculos. Para calcular la diferencia entre fechas utilice el método `diff()`.
Este devolverá un `new DateInterval`, el cual puede ser fácilmente impreso en la pantalla.

{% highlight php %}
<?php
// Se crea una copia de $inicio y se le añade un mes y 6 días.
$fin = clone $start;
$fin->add(new DateInterval('P1M6D'));

$diff = $fin->diff($inicio);
echo "Diferencia: " . $diff->format('%m mes, %d días (total: %a días)') . PHP_EOL;
// Diferencia: 1 mes, 6 días (total: 37 días)
{% endhighlight %}

Es posible comparar fácilmente los objetos DateTime:

{% highlight php %}
<?php
if($inicio < $fin) {
    echo "¡El inicio sucede antes que el final!\n";
}
{% endhighlight %}

Este último ejemplo demuestra cómo se utiliza la clase DatePeriod para iterar sobre eventos periódicos. Este puede tomar
dos objetos DateTime, uno para el inicio y el otro para el final, y el intervalo que define el número de eventos periódicos que se devuelven.


{% highlight php %}
<?php
// Imprimir todos los jueves entre $inicio y $fin
$intervaloDePeriodo = \DateInterval::createFromDateString('first thursday');
$iteradorDePeriodo = new \DatePeriod($inicio, $intervaloDePeriodo, $fin, \DatePeriod::EXCLUDE_START_DATE);
foreach($iteradorDePeriodo as $fecha)
{
    // Imprimir cada fecha en el periodo
    echo $fecha->format('m/d/Y') . " ";
}
{% endhighlight %}

Una extensión popular del API de PHP es [Carbon](https://carbon.nesbot.com/). Esta hereda todo lo de la clase DateTime, por lo que requiere cambios mínimos del código,
pero incluye características adicionales, como el soporte de localización, muchas más forma de sumar, restar y formatear los objetos DateTime, además de medios para
probar  código gracias a que permite simular cualquier fecha y hora que se desee.


* [Leer acerca de la clase DateTime][datetime]
* [Como formatear la fecha][dateformat] (Opciones de los formatos aceptados para una fecha)

[datetime]: https://php.net/manual/es/book.datetime.php
[dateformat]: https://php.net/manual/es/function.date.php

