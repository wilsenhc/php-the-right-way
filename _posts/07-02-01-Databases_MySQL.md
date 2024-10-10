---
title:   Extensión MySQL
isChild: true
anchor:  extension_mysql
---

## Extensión MySQL {#extension_mysql_title}

La extensión [mysql] para PHP es increíblemente antigua y ha sido reemplazada por otras dos extensiones:

- [mysqli]
- [pdo]

No sólo el desarrollo de [mysql] se detuvo hace mucho tiempo, sino que además
**ha sido [oficialmente eliminado en PHP 7.0][mysql_removed]**.

Para ahorrarse la búsqueda en su `php.ini` para ver qué módulo está utilizando, una opción es buscar `mysql_*`
en el editor de su elección. Si aparecen funciones como `mysql_connect()` y `mysql_query()`, entonces está usando `mysql`.

Incluso si aún no está utilizando PHP 7.x o posterior, no considerar esta actualización lo antes posible le acarreará mayores
dificultades cuando se produzca la actualización de PHP. La mejor opción es reemplazar el uso de mysql por [mysqli] o [PDO] en tus
aplicaciones dentro de tus propios calendarios de desarrollo para que no te veas apurado más adelante.

**Si está actualizando de [mysql] a [mysqli], tenga cuidado con las guías de actualización perezosas que sugieren que simplemente puede encontrar y reemplazar `mysql_*` con `mysqli_*`. No sólo es una simplificación excesiva, sino que pierde las ventajas que mysqli proporciona, como la vinculación de parámetros, que también se ofrece en [PDO][pdo].**

* [Sentencias Preparadas de MySQLi][mysqli_prepared_statements]
* [PHP: Cómo elegir una API para MySQL][mysql_api]

[mysql]: https://www.php.net/mysqli
[mysql_removed]: https://www.php.net/manual/migration70.removed-exts-sapis.php
[mysqli]: https://www.php.net/mysqli
[pdo]: https://www.php.net/pdo
[mysql_api]: https://www.php.net/mysqlinfo.api.choosing
[mysqli_prepared_statements]: https://websitebeaver.com/prepared-statements-in-php-mysqli-to-prevent-sql-injection
