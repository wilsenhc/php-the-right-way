---
title: Bases de Datos
---

# Bases de Datos

Muchas veces su código PHP utilizara una base de datos para persistir información. Hay algunas opciones para conectarse e interactuar con la base de datos. La opcion recomendable, _hasta PHP 5.1.0_, era el utilizar los controladores nativos como [mysql][mysql], [mysqli][mysqli], [pgsql][pgsql], y otros.

Los controladores nativos son excelentes si solamente estara utilizando UNA SOLA base de datos en su aplicación, pero si, por ejemplo, esta utilizando MySQL y un poco de MSSQL, o necesita conectarse a una base de datos Oracle, entonces no podrá utilizar los mismos controladores. Necesita aprender un nuevo API para cada base de datos &mdash; y eso puede ser frustrante.

Algo adicional sobre los controladores nativos: la extensión `mysql` para PHP ya no está siendo actualizada y el estatus oficial de ella desde PHP 5.4.0 es la de "Eliminación a Largo Plazo". Esto quiere decir que la extensión será eliminada en los próximos lanzamientos, así que en PHP 5.6 (o lo que viene después de 5.5) puede que ya no exista. Si usted está usando `mysql_connect()` y `mysql_query()` en sus aplicaciones es posible que tenga que reemplazar su código en el futuro, así que la mejor opción es empezar a usar `mysqli` o la librería PDO de ahora en adelante. _Si esta comenzando de cero entonces no utilice la extensión `mysql` en absoluto_. Utilice la [extensión MySQLi][mysqli], o la librería PDO.

* [PHP: Elegir una API para MySQL](http://php.net/manual/es/mysqlinfo.api.choosing.php)

[mysql]: http://php.net/manual/es/mysql
[mysqli]: http://php.net/manual/es/book.mysqli.php
[pgsql]: http://php.net/manual/es/book.pgsql.php

## PDO

PDO (Objetos de Datos de PHP) es una librería de abstracción para establecer conexiones a bases de datos &mdash; incluida en PHP desde la versión 5.1.0 &mdash; que provee una interface común para comunicarse con diferentes sistemas de bases de datos. PDO no interpreta sus consultas en SQL ni emula características que faltan; solo se utiliza para establecer conexiones a diferentes bases de datos con el mismo API.

Lo que es más importante, PDO le permite inyectar la entrada de datos de forma segura en sus consultas de SQL sin tener que preocuparse de sufrir ataques de inyección de SQL en su base de datos. Esto es posible gracias a las declaraciones y los parámetros consolidados de PDO.

Supongamos que un programa de PHP recibe un ID numérico en la forma de un parámetro de consulta. Este ID debe ser utilizado para extraer un registro de usuario de una base de datos. El ejemplo que sigue muestra la manera *incorrecta* de hacerlo:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:usuarios.db');
$pdo->query("SELECT nombre FROM usuarios WHERE id = " . $_GET['id']); // <-- No!
{% endhighlight %}

Esta es la peor manera de hacerlo, ya que se está insertando el parámetro directamente, o sin “sanear”, a la consulta de SQL y sin usar parámetros consolidados provistos por PDO. Veamos un mejor ejemplo:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:usuarios.db');
$stmt = $pdo->prepare('SELECT nombre FROM usuarios WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); //<-- Automatically sanitized by PDO
$stmt->execute();
{% endhighlight %}

Esta es la manera correcta porque se usa un parámetro consolidado en una declaración de PDO. Esto sanea la entrada de datos antes de que se introduzca en la base de datos, así previniendo un probable ataque de inyección de SQL.

* [Aprenda más acerca de PDO][1]

[1]: http://www.php.net/manual/es/book.pdo.php

## Capas de Abstracción

Muchos de los armazones de desarrollo disponibles proveen su propia capa de abstracción que puede o no usar PDO como base. Estas capas muy a menudo emulan las características y diferencias entre un sistema de base de datos y otro al envolver las consultas en métodos de PHP, lo que proporciona una abstracción efectiva de la base de datos. Claramente, esto añade una pequeña sobrecarga a su proyecto, pero si está tratando de desarrollar una aplicación portable que necesite trabajar con MySQL, PostgreSQL y SQLite entonces esa pequeña sobrecarga valdrá la pena ya que mantendrá su código limpio y con una estructura elegante.

Algunas capas de abstracción han sido desarrolladas con el estándar PSR-0  para uso de espacios de nombres en mente, lo cual facilita la configuración en cualquiera de sus proyectos (La siguiente documentación solo está disponible en inglés):

* [Doctrine2 DBAL][2]
* [ZF2 Db][4]
* [ZF1 Db][3]


[2]: http://www.doctrine-project.org/projects/dbal.html
[3]: http://framework.zend.com/manual/en/zend.db.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/zend.db.html
