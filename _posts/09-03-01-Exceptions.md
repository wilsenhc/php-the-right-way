---
title:   Excepciones
isChild: true
anchor:  excepciones
---

## Excepciones {#excepciones_title}

Las excepciones son una parte estándar de la mayoría de los lenguajes de programación populares,
pero a menudo son pasadas por alto por los programadores de PHP. Lenguajes como Ruby son extremadamente dependientes de
excepciones, así que cada vez que algo sale mal, como una falla en una solicitud HTTP, un error en una consulta a
la base de datos, o incluso si no se puede encontrar un recurso de imagen, Ruby (o las gems utilizadas) lanzará una excepción
a la pantalla, lo que significa que instantáneamente sabrás que hay un error.

PHP, por su parte, es bastante indulgente con esto, y una llamada a `file_get_contents()` generalmente solo te devolverá
un `FALSE` y un `warning`. Muchos frameworks antiguos de PHP, como CodeIgniter, simplemente devolverán un falso,
registrarán un mensaje en sus registros y tal vez te permitan usar un método como $this->upload->get_error() para ver
qué salió mal. El problema aquí es que tienes que ir a buscar un error y consultar la documentación para ver cuál es
el método de error para esta clase, en lugar de que se te haga extremadamente obvio.

Otro problema es cuando las clases lanzan automáticamente un error en la pantalla y terminan el proceso.
Cuando haces esto, detienes a otro desarrollador de poder manejar dinámicamente ese error.
Las excepciones deben lanzarse para hacer que un desarrollador sea consciente de un error;
luego puede elegir cómo manejarlo. Por ejemplo:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // La validación falló
}
catch(Fuel\Email\SendingFailedException $e)
{
    // El controlador no pudo enviar el correo electrónico
}
finally
{
    // Ejecutado independientemente de si se ha lanzado una excepción, y antes de que se reanude la ejecución normal
}
{% endhighlight %}

### Excepciones SPL

La clase genérica `Exception` proporciona muy poco contexto de depuración para el desarrollador; sin embargo, 
para remediar esto, es posible crear un tipo de `Exception` especializado al sub-clasificar la clase genérica `Exception`:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

Esto significa que puedes agregar múltiples bloques de captura y manejar diferentes excepciones de manera diferente. 
Esto puede llevar a la creación de un <em>gran</em> número de Excepciones personalizadas, 
algunas de las cuales podrían haberse evitado utilizando las excepciones SPL proporcionadas en la [extensión SPL][splext]. 

Si, por ejemplo, utilizas el método mágico `__call()` y se solicita un método no válido, en lugar de lanzar una 
Excepción estándar que es vaga, o crear una Excepción personalizada solo para eso, 
podrías simplemente `throw new BadMethodCallException;`.

* [Lee sobre Excepciones][exceptions]
* [Lee sobre Excepciones SPL][splexe]
* [Nidificación de Excepciones en PHP][nesting-exceptions-in-php]


[splext]: /#standard_php_library
[exceptions]: https://www.php.net/language.exceptions
[splexe]: https://www.php.net/spl.exceptions
[nesting-exceptions-in-php]: https://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
