---
title:   Interacción con Bases de Datos
isChild: true
anchor:  interaccion_con_bases_de_datos
---

## Interacción con Bases de Datos {#interaccion_con_bases_de_datos_title}

Cuando los desarrolladores comienzan a aprender PHP, a menudo terminan mezclando su interacción con la base de datos con su
lógica de presentación, utilizando código que podría parecerse a esto:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
?>
</ul>
{% endhighlight %}

Esta es una mala práctica por todo tipo de razones, principalmente que es difícil de depurar, difícil de probar, difícil de leer
y que va a dar salida a un montón de campos si no pones un límite.

Aunque hay muchas otras soluciones para hacer esto - dependiendo de si prefieres [POO](/#programación-orientada-a-objetos) o [programación funcional](/#programación-funcional) - debe haber algún elemento de separación.

Considere el paso más básico:

{% highlight php %}
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

$results = getAllFoos($db);
foreach ($results as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
{% endhighlight %}

Es un buen comienzo. Pon esos dos elementos en dos archivos diferentes y tendrás una separación limpia.

Crea una clase en la que colocar ese método y tendrás un "Modelo". Crea un simple archivo `.php` para colocar
la lógica de presentación y tendrás una "Vista", que es muy parecido a [MVC] - una arquitectura OOP común para
la mayoría de los [frameworks](/#frameworks).

**foo.php**

{% highlight php %}
<?php
$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8mb4', 'username', 'password');

// Ponga su modelo a disposición
include 'models/FooModel.php';

// Crear una instancia
$fooModel = new FooModel($db);
// Obtener la lista de Foos
$fooList = $fooModel->getAllFoos();

// Mostrar la vista
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class FooModel
{
    public function __construct(protected PDO $db)
    {
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<?php foreach ($fooList as $row): ?>
    <li><?= $row['field1'] ?> - <?= $row['field1'] ?></li>
<?php endforeach ?>
{% endhighlight %}

Esto es esencialmente lo mismo que hacen la mayoría de los frameworks modernos, aunque un poco más manual.
Puede que no necesites hacer todo eso cada vez, pero mezclar demasiada lógica de presentación e interacción con la base de datos
puede ser un verdadero problema si alguna vez quieres hacer [test unitarios](/#test-unitarios) a tu aplicación.


[MVC]: https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
