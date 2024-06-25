---
title:  Guía de Estilos del Código
anchor: guia_de_estilos_del_codigo
---

# Guía de Estilos del Código {#guia_de_estilos_del_codigo_title}

La comunidad PHP es grande y diversa, compuesta por innumerables bibliotecas, frameworks y componentes. Es habitual que
los desarrolladores de PHP elijan varios de ellos y los combinen en un único proyecto. Es importante que el código PHP se adhiera
(tanto como sea posible) a un estilo de código común para facilitar a los desarrolladores mezclar y combinar
varias librerías para sus proyectos.

El [Framework Interop Group][fig] ha propuesto y aprobado una serie de recomendaciones de estilo. No todas están relacionadas
con el estilo del código, pero las que sí lo hacen son [PSR-1][psr1], [PSR-12][psr12], [PSR-4][psr4] y [PER Coding Style][per-cs].
Estas recomendaciones no son más que un conjunto de reglas que muchos proyectos como Drupal, Zend, Symfony, Laravel, CakePHP,
phpBB, AWS SDK, FuelPHP, Lithium, etc. adoptan. Puedes utilizarlas para tus propios proyectos, o seguir utilizando tu estilo personal.

Lo ideal sería escribir código PHP que se adhiera a un estándar conocido. Esto podría ser cualquier combinación de PSRs, o uno
de los estándares de codificación hechos por PEAR o Zend. Esto significa que otros desarrolladores pueden leer y trabajar
fácilmente con su código, y las aplicaciones que implementan los componentes pueden tener consistencia incluso cuando se trabaja con mucho código de terceros.

* [Leer más sobre PSR-1][psr1]
* [Leer más sobre PSR-12][psr12]
* [Leer más sobre PSR-4][psr4]
* [Leer más sobre PER Coding Style][per-cs]
* [Leer más sobre PEAR Coding Standards][pear-cs]
* [Leer más sobre Symfony Coding Standards][symfony-cs]

Puedes usar [PHP_CodeSniffer][phpcs] para comprobar el código contra cualquiera de estas recomendaciones, y plugins para editores
de texto como [Sublime Text][st-cs] para recibir feedback en tiempo real.

Puede corregir la estructura del código automáticamente utilizando una de las siguientes herramientas:

- Uno es el [PHP Coding Standards Fixer][phpcsfixer] que tiene una base de código muy bien probada.
- También puede usar la herramienta [PHP Code Beautifier and Fixer][phpcbf] que se incluye con PHP_CodeSniffer para ajustar su código de forma adecuada.

Y puedes ejecutar phpcs manualmente desde el shell:

    phpcs -sw --standard=PSR1 file.php

Mostrará los errores y describirá cómo solucionarlos.
También puede ser útil incluir el comando `phpcs` en un git pre-commit hook con el argumento CLI `--filter=GitStaged`.
De este modo, el código que contenga errores contra la norma elegida no podrá entrar en el repositorio hasta que los
errores hayan sido corregidos.

Si tiene PHP_CodeSniffer, puede arreglar los problemas de estructura del código reportados por esta herramienta automáticamente,
con [PHP Code Beautifier and Fixer][phpcbf].

    phpcbf -w --standard=PSR1 file.php

Otra opción es usar el [PHP Coding Standards Fixer][phpcsfixer].
Mostrará qué tipo de errores tenía la estructura del código antes de corregirlos.

    php-cs-fixer fix -v --rules=@PSR1 file.php

Se prefiere el inglés para todos los nombres de símbolos e infraestructura de códigos. Los comentarios pueden redactarse
en cualquier idioma fácilmente legible por todas las partes actuales y futuras que puedan trabajar en el código base.

Por último, un buen recurso complementario para escribir código PHP limpio es [Clean Code PHP][cleancode].

[fig]: https://www.php-fig.org/
[psr1]: https://www.php-fig.org/psr/psr-1/
[psr12]: https://www.php-fig.org/psr/psr-12/
[psr4]: https://www.php-fig.org/psr/psr-4/
[per-cs]: https://www.php-fig.org/per/coding-style/
[pear-cs]: https://pear.php.net/manual/en/standards.php
[symfony-cs]: https://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: https://github.com/PHPCSStandards/PHP_CodeSniffer
[phpcbf]: https://github.com/PHPCSStandards/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: https://cs.symfony.com/
[cleancode]: https://github.com/jupeter/clean-code-php
