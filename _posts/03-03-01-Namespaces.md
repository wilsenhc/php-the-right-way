---
title:   Namespaces
isChild: true
anchor:  namespaces
---

## Namespaces {#namespaces_title}

Como se mencionó anteriormente, la comunidad PHP tiene muchos desarrolladores creando mucho código. Esto significa que el código PHP
de una biblioteca puede usar el mismo nombre de clase que otra. Cuando ambas bibliotecas son usadas en el mismo espacio de nombres,
estas colisionan y causan problemas.

Los _espacios de nombres_ (Namespaces) resuelven este problema. Como se describe en el manual de referencia de PHP, los espacios de nombres pueden compararse con los directorios del sistema operativo que _espacian_ o _separan_ los archivos; dos archivos con el mismo nombre pueden coexistir en directorios separados.
Del mismo modo, dos clases PHP con el mismo nombre pueden coexistir en espacios de nombres PHP separados. Así de simple.

Es importante que asigne un espacio de nombres a su código para que pueda ser utilizado por otros desarrolladores
sin temor a colisionar con otras bibliotecas.

Una forma recomendada de utilizar los espacios de nombres es la descrita en [PSR-4][psr4], cuyo objetivo es proporcionar
una convención estándar de archivos, clases y espacios de nombres para permitir un código plug-and-play.

En octubre de 2014 el PHP-FIG dejó obsoleto el anterior estándar de autocarga: [PSR-0][psr0]. Tanto PSR-0 como PSR-4 siguen siendo perfectamente utilizables.
Este último requiere PHP 5.3, por lo que muchos proyectos que solo usan PHP 5.2 implementan PSR-0.

Si va a utilizar un estándar de autocargador para una nueva aplicación o paquete, considere utilizar PSR-4.

* [Leer más sobre Namespaces][namespaces]
* [Leer más sobre PSR-0][psr0]
* [Leer más sobre PSR-4][psr4]


[namespaces]: https://www.php.net/language.namespaces
[psr0]: https://www.php-fig.org/psr/psr-0/
[psr4]: https://www.php-fig.org/psr/psr-4/
