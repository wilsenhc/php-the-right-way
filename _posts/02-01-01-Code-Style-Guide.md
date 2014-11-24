---
title: Guía de Estilo de Código
anchor: guia-de-estilo-del-codigo
---

# Guía de Estilo de Código {#guia-de-estilo-del-codigo}

La comunidad detrás de PHP es enorme y diversa, compuesta de innumerables librerías, armazones de desarrollo (*frameworks*) y componentes. Es común que desarrolladores en PHP escojan de entre estos  y los combinen en un solo proyecto. Por eso es importante que el código PHP se adhiera (lo más cerca posible) a un estilo de código común para que se facilite el trabajo de los desarrolladores al combinar una variedad de librerías para sus proyectos.

El [Framework Interop Group][fig] (antes conocido como el 'PHP Standards Group') ha propuesto y aprobado una serie de recomendaciones de estilo, conocidas como [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] y [PSR-4][psr4]. No deje que los títulos raros lo confundan, estas recomendaciones son simplemente un conjunto de normas que algunos proyectos como Drupal, Zend, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium, y otros han comenzado a adoptar. Usted puede utilizar estas normas en sus propios proyectos o continuar usando su propio estilo.

Sería ideal que escribiera código PHP que se adhiere a uno o más de estos estándares. Puede ser cualquier combinación de PSR, o uno de los estándares de codificación hechos por PEAR o Zend. Esto significa que otros desarrolladores pueden fácilmente leer y trabajar con su código, y las aplicaciones que implementan los componentes puedan tener consistencia incluso cuando trabajen con una gran cantidad de código de terceros.

* [Lea acerca de PSR-0][psr0]
* [Lea acerca de PSR-1][psr1]
* [Lea acerca de PSR-2][psr2]
* [Lea acerca de PSR-4][psr4]
* [Lea acerca de los Estandares de Codificación de PEAR][pear-cs]
* [Lea acerca de los Estandares de Codificación de Zend][zend-cs]
* [Lea acerca de los Estandares de Codificación de Symfony][symfony-cs]

Puede utilizar [PHP_CodeSniffer][phpcs] para verificar que su código se apegue a estas recomendaciones, y plugins para editores de texto como [Sublime Text 2][st-cs] para obtener un análisis en tiempo real.

Utilice [PHP Coding Standards Fixer][phpcsfixer] de Fabien Potencier para modificar la sintaxis de su código automáticamente y así quede conforme a estos estándares, ahorrándole tiempo y esfuerzo que requeriría arreglar cada problema a mano.

Se prefiere la utilización del idioma Inglés para todos los nombres de símbolos e infraestructura del código. Los comentarios pueden ser escritos e un lenguaje fácilmente legible para todos autores y futuros desarrolladores que trabajaran en la base del código.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
