---
title:  Bases de Datos
anchor: bases_de_datos
---

# Bases de Datos {#bases_de_datos_title}

Muchas veces su código PHP utilizará una base de datos para persistir información. Tiene algunas opciones para conectarse
e interactuar con su base de datos. La opción recomendada **hasta PHP 5.1.0** era usar controladores nativos como [mysqli],
[pgsql], [mssql], etc.

Los drivers nativos son geniales si sólo estás usando _una_ base de datos en tu aplicación, pero si, por ejemplo, estás usando MySQL
y un poco de MSSQL, o necesitas conectarte a una base de datos Oracle, entonces no podrás usar los mismos drivers.
Tendrás que aprender una API completamente nueva para cada base de datos &mdash; y eso puede llegar a ser una tontería.


[mysqli]: https://www.php.net/mysqli
[pgsql]: https://www.php.net/pgsql
[mssql]: https://www.php.net/mssql
