---
title: Composer y Packagist
anchor: composer-y-packagist
isChild: true
---

## Composer y Packagist

Composer es un **excelente** gestor de dependencias para PHP. Solo tienes que añadir las dependencias de tu proyecto a un archivo llamado `composer.json`, ejecutar algunos comandos y Composer descargará automáticamente las dependencias para el proyecto y configurará el cargador automático en cuestión de segundos.

Ya existen muchas librerías PHP compatibles con Composer y están listas para que las uses en tus proyectos. Hay una lista de estos “paquetes” en el sitio [Packagist][1], que es el repositorio oficial de librerías compatibles con Composer.

### Como configurar Composer

Se puede instalar Composer localmente (en el directorio de trabajo actual, aunque esto ya no es recomendable) o globalmente (por ejemplo, en /user/local/bin). Supongamos que quieres configurar Composer localmente. Desde el directorio raíz de tu proyecto:

    curl -s http://getcomposer.org/installer | php

Esto descargará el archivo binario `composer.phar`. Se puede ejecutar este archivo con `php` para manejar las dependencias de tu proyecto. *Por favor, ten en cuenta que:* Si ejecutas el código directamente en el intérprete de PHP al mismo tiempo que lo descargas, deberías leer cuidadosamente el código descargado del programa con anterioridad y confirmar que es seguro.

### Como configurar Composer (manualmente)

Configurar Composer manualmente requiere técnicas avanzadas. No obstante, hay varias razones por las cuales un desarrollador como tú prefiera configurarlo de esta manera en vez de utilizar la rutina de configuración interactiva. La configuración interactiva verifica tu sistema de PHP para asegurar que:

- Está utilizando una versión compatible de PHP
- Los archivos `.phar` pueden ser ejecutados correctamente
- Tiene suficientes permisos en los directorios
- Algunas extensiones que pueden causar problemas no han sido cargadas
- El archivo `php.ini` tiene los ajustes necesarios

Ya que la configuración manual no realiza ninguna de estas verificaciones, necesitas tomar en consideración si tal funcionamiento es lo que deseas. De todas maneras, puedes obtener y configurar Composer manualmente de la siguiente manera:

    curl -s http://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

La ruta `$HOME/local/bin` (o un directorio que escojas) necesita estar en el variable de entorno `$PATH`. De esta manera, el comando `composer` estará habilitado en cualquier directorio del sistema.

Cuando encuentres instrucciones que sugieran ejecutar Composer con `php composer.phar install`, esto se puede sustituir con:

    composer install

### Como Definir y Configurar Dependencias

Primero, se crea un archivo `composer.json` en el mismo directorio donde se encuentra `composer.phar`. Enseguida, encontramos un ejemplo que define el paquete [Twig][2] como una dependencia del  proyecto:

	{
	    "require": {
	        "twig/twig": "1.8.*"
	    }
	}

El siguiente paso es ejecutar Composer desde el directorio raíz de tu proyecto:

    php composer.phar install

Esto descargará y configurará la dependencia dentro de un directorio llamado `vendors/`. Una vez configurado, añade esta línea de código al archivo principal de tu aplicación:

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Esta instrucción le dice al programa que use el cargador automático de Composer para cargar cualquier dependencia que hayas configurado. Ahora tus dependencias serán cargadas dinámicamente según tu programa las requiera.

* [Aprenda más acerca de Composer][3]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: http://getcomposer.org/doc/00-intro.md
