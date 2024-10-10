---
title:   Extensión PDO
isChild: true
anchor:  extension_pdo
---

## Extensión PDO {#extension_pdo_title}

[PDO] es una librería de abstracción de conexión a bases de datos &mdash; incorporada en PHP desde 5.1.0 &mdash; que proporciona
una interfaz común común para hablar con muchas bases de datos diferentes. Por ejemplo, puede utilizar código básicamente idéntico
para interactuar con MySQL o SQLite:

{% highlight php %}
<?php
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO no traducirá sus consultas SQL o emulará las características que faltan; es puramente para la conexión a múltiples tipos
de base de datos con la misma API.

Y lo que es más importante, `PDO` le permite inyectar de forma segura entradas ajenas (por ejemplo, IDs) en sus consultas SQL sin preocuparse
por ataques de inyección SQL a bases de datos.
Esto es posible utilizando sentencias PDO y parámetros vinculados.

Supongamos que un script PHP recibe un ID numérico como parámetro de consulta. Este ID debe ser usado para obtener un registro
de usuario de una base de datos. Esta es la forma `incorrecta` de hacer esto:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Este código es terrible. Estás insertando un parámetro de consulta sin procesar en una consulta SQL. Esto hará que te hackeen en un santiamén, usando una práctica llamada [Inyección SQL][SQL Injection]. Imagínese si un hacker pasa un parámetro `id` inventivo
llamando a una URL como `http://domain.com/?id=1%3BDELETE+FROM+users`. Esto establecerá la variable `$_GET['id']` a
`1;DELETE FROM users` lo que borrará todos los usuarios. En su lugar, debería desinfectar/sanitizar la entrada de ID utilizando
parámetros vinculados a PDO.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$id = filter_input(INPUT_GET, 'id', FILTER_SANITIZE_NUMBER_INT); // <-- filtre primero los datos (ver [Filtrado de Datos](#filtrado_de_datos)), especialmente importante para INSERT, UPDATE, etc.
$stmt->bindParam(':id', $id, PDO::PARAM_INT); // <-- SQL saneado automáticamente por PDO
$stmt->execute();
{% endhighlight %}

Este código es correcto. Utiliza un parámetro vinculado en una sentencia PDO. Esto escapa el ID de entrada externo
antes de que sea introducido en la base de datos previniendo potenciales ataques de inyección SQL.

Para escrituras, como INSERT o UPDATE, es especialmente crítico [filtrar sus datos](#filtrado_de_datos) primero y sanearlos para otras cosas (eliminación de etiquetas HTML, JavaScript, etc).  PDO sólo lo desinfectará para SQL, no para su aplicación.

* [Más información sobre PDO][pdo]

También hay que tener en cuenta que las conexiones a bases de datos consumen recursos y no era raro que se agotaran los recursos
si las conexiones no se cerraban implícitamente, aunque esto era más común en otros lenguajes. Usando PDO puedes cerrar implícitamente
la conexión destruyendo el objeto asegurándote de que todas las referencias restantes a él son borradas, es decir, establecidas a NULL.
Si no hace esto explícitamente, PHP cerrará automáticamente la conexión cuando su script termine -
a menos que esté usando conexiones persistentes.

* [Más información sobre las conexiones PDO][Learn about PDO connections]


[pdo]: https://www.php.net/pdo
[SQL Injection]: https://web.archive.org/web/20210413233627/http://wiki.hashphp.org/Validation
[Learn about PDO connections]: https://www.php.net/pdo.connections
