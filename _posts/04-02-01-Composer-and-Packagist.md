---
title:   Composer y Packagist
isChild: true
anchor:  composer_y_packagist
---

## Composer y Packagist {#composer_y_packagist_title}

Composer es el gestor de dependencias recomendado para PHP. Enumera las dependencias de tu proyecto en un archivo `composer.json` y,
con unos simples comandos, Composer descargará automáticamente las dependencias de tu proyecto y configurará la carga automática por ti.
Composer es análogo a NPM en el mundo node.js, o Bundler en el mundo Ruby.

Existe una plétora de librerías PHP compatibles con Composer y listas para ser utilizadas en tu proyecto. Estos "paquetes" están listados en [Packagist], el repositorio oficial de librerías PHP compatibles con Composer.

### Cómo instalar Composer

La forma más segura de descargar Composer es [siguiendo las instrucciones oficiales](https://getcomposer.org/download/).
Esto verificará que el instalador no está corrupto o manipulado.
El instalador instala un binario `composer.phar` en su _directorio de trabajo actual_.

Recomendamos instalar Composer *globalmente* (por ejemplo, una única copia en `/usr/local/bin`). Para ello, ejecute este comando a continuación:

{% highlight console %}
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

**Nota:** Si lo anterior falla por los permisos, prefijar con `sudo`.

Para ejecutar un Composer instalado localmente se usaría `php composer.phar`, globalmente es simplemente `composer`.

#### Instalar en Windows

Para los usuarios de Windows la forma más fácil de empezar a funcionar es utilizar el instalador [ComposerSetup], que
realiza una instalación global y configura tu `$PATH` para que puedas llamar a `composer` desde cualquier directorio en tu línea de comandos.

### Cómo Definir e Instalar Dependencias

Composer mantiene un registro de las dependencias de tu proyecto en un archivo llamado `composer.json`. Puedes gestionarlo
manualmente si lo deseas, o utilizar el propio Composer. El comando `composer require` añade una dependencia del proyecto y si no
tienes un archivo `composer.json`, se creará uno. Aquí tienes un ejemplo que añade [Twig] como dependencia de tu proyecto.

{% highlight console %}
composer require twig/twig:^2.0
{% endhighlight %}

Como alternativa, el comando `composer init` le guiará a través de la creación de un archivo completo `composer.json` para su proyecto.
De cualquier manera, una vez que haya creado su archivo `composer.json` puede decirle a Composer que descargue e instale sus dependencias en el directorio `vendor/`.
Esto también se aplica a los proyectos que ha descargado que ya proporcionan un archivo `composer.json`:

{% highlight console %}
composer install
{% endhighlight %}

A continuación, añada esta línea al archivo PHP principal de su aplicación; esto le dirá a PHP que utilice el autocargador (del Inglés "autoloader") de Composer para las dependencias de su proyecto.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Ahora puedes utilizar las dependencias de tu proyecto y se cargarán automáticamente cuando las necesites.

### Actualizar las dependencias

Composer crea un archivo llamado `composer.lock` que almacena la versión exacta de cada paquete que descargó
cuando ejecutó por primera vez `composer install`. Si comparte su proyecto con otros,
asegúrese de que el archivo `composer.lock` esté incluido, de modo que cuando ejecuten `composer install` obtengan
las mismas versiones que usted.  Para actualizar sus dependencias, ejecute `composer update`. No utilice
`composer update` al desplegar, sólo `composer install`,
de lo contrario puede terminar con diferentes versiones de paquetes en producción.

Ts muy útil cuando se definen los requisitos de versión de forma flexible. Por ejemplo, un requisito de versión de `~1.8` significa
"cualquier cosa más nueva que `1.8.0`, pero menos que `2.0.x-dev`". También puede utilizar el comodín `*` como en `1.8.*`.
Ahora el comando `composer update` de Composer actualizará todas tus dependencias a la versión más reciente que se ajuste a las restricciones que definas.

### Notificaciones de Actualización

Para recibir notificaciones sobre el lanzamiento de nuevas versiones puede suscribirse a [libraries.io], un servicio web
que puede supervisar las dependencias y enviarle alertas sobre las actualizaciones.

### Comprobar la seguridad de las dependencias

El [Comprobador Local de Seguridad PHP][Local PHP Security Checker] (en Inglés "Local PHP Security Checker")
es una herramienta de línea de comandos, que examinará su archivo `composer.lock`
y le dirá si necesita actualizar alguna de sus dependencias.

### Gestión de dependencias globales con Composer

Composer también puede gestionar dependencias globales y sus binarios. El uso es sencillo, todo lo que necesitas hacer
es anteponer a su comando con `global`. Si por ejemplo quieres instalar PHPUnit y tenerlo
disponible globalmente, ejecutarías el siguiente comando:

{% highlight console %}
composer global require phpunit/phpunit
{% endhighlight %}

Esto creará una carpeta `~/.composer` donde residen tus dependencias globales. Para que los binarios de los paquetes instalados,
añada la carpeta `~/.composer/vendor/bin` a la variable `$PATH`.

* [Más información sobre Composer][Learn about Composer]

[Packagist]: https://packagist.org/
[Twig]: https://twig.symfony.com/
[libraries.io]: https://libraries.io/
[Local PHP Security Checker]: https://github.com/fabpot/local-php-security-checker
[Learn about Composer]: https://getcomposer.org/doc/00-intro.md
[ComposerSetup]: https://getcomposer.org/Composer-Setup.exe
