---
title:   Capas de Abstracción
isChild: true
anchor:  capas_de_abstraccion_de_bases_de_datos
---

## Capas de Abstracción {#capas_de_abstraccion_de_bases_de_datos_title}

Muchos frameworks proporcionan su propia capa de abstracción que puede o no sentarse encima de [PDO][1].
Estos a menudo emulan características de un sistema de base de datos que falta en otro envolviendo sus consultas en métodos PHP,
dándole abstracción de base de datos real en lugar de sólo la abstracción de conexión que PDO proporciona. Esto, por supuesto,
añadirá un poco de sobrecarga, pero si usted está construyendo una aplicación portable que necesita trabajar con MySQL,
PostgreSQL y SQLite entonces un poco de sobrecarga valdrá la pena por el bien de la limpieza del código.

Algunas capas de abstracción se han construido utilizando los estándares de espacio de nombres [PSR-0][psr0] o [PSR-4][psr4], por lo que pueden instalarse en cualquier aplicación que se desee:

* [Atlas][5]
* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Medoo][8]
* [Propel][7]
* [laminas-db][4]


[1]: https://www.php.net/book.pdo
[2]: https://www.doctrine-project.org/projects/dbal.html
[4]: https://docs.laminas.dev/laminas-db/
[5]: https://atlasphp.io
[6]: https://github.com/auraphp/Aura.Sql
[7]: https://propelorm.org/
[8]: https://medoo.in/
[psr0]: https://www.php-fig.org/psr/psr-0/
[psr4]: https://www.php-fig.org/psr/psr-4/
