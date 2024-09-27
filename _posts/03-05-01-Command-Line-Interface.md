---
title:   Interfaz de Línea de Comandos (CLI)
isChild: true
anchor:  interfaz_de_linea_de_comandos
---

## Interfaz de Línea de Comandos (CLI) {#interfaz_de_linea_de_comandos_title}

PHP fue creado para escribir aplicaciones web, pero también es útil para scripting de programas de interfaz de línea de comandos (CLI).
Los programas PHP de línea de comandos pueden ayudar a automatizar tareas comunes como pruebas, despliegue y administración de aplicaciones.

Los programas PHP CLI son poderosos porque puedes usar el código de tu aplicación directamente sin tener que crear y asegurar una web
GUI para ella. ¡Solo asegúrate de **no** poner tus scripts PHP CLI en tu raíz web pública!

Intente ejecutar PHP desde su línea de comandos:

{% highlight console %}
> php -i
{% endhighlight %}

La opción `-i` imprimirá su configuración PHP igual que la función [`phpinfo()`][phpinfo].

La opción `-a` proporciona un shell interactivo, similar al IRB de ruby o al shell interactivo de python. También existen
de otras útiles [opciones de línea de comandos][cli-options], también.

Escribamos un simple programa CLI «Hola, $nombre». Para probarlo, crea un archivo llamado `hello.php`, como se muestra a continuación.

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Como usar: php hello.php <name>" . PHP_EOL;
    exit(1);
}
$name = $argv[1];
echo "Hola, $name" . PHP_EOL;
{% endhighlight %}

PHP establece dos variables especiales basadas en los argumentos con los que se ejecuta el script. [`$argc`][argc] es una variable entera
que contiene el *conteo* de argumentos y [`$argv`][argv] es una variable array que contiene el *valor* de cada argumento.
El primer argumento es siempre el nombre de su archivo de script PHP, en este caso `hello.php`.

La expresión `exit()` se utiliza con un número distinto de cero para hacer saber al shell que el comando ha fallado. Los códigos de salida más comunes se pueden encontrar [aquí][exit-codes].

Para ejecutar nuestro script, antes visto, desde la línea de comandos:

{% highlight console %}
> php hello.php
Como usar: php hello.php <name>
> php hello.php mundo
Hola, mundo
{% endhighlight %}


 * [Aprenda a ejecutar PHP desde la línea de comandos][php-cli]

[phpinfo]: https://www.php.net/function.phpinfo
[cli-options]: https://www.php.net/features.commandline.options
[argc]: https://www.php.net/reserved.variables.argc
[argv]: https://www.php.net/reserved.variables.argv
[exit-codes]: https://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: https://www.php.net/manual/en/features.commandline.php
