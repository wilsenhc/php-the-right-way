---
title:   Concepto Básico
isChild: true
anchor:  concepto_basico
---

## Concepto Básico {#concepto_basico_title}

Podemos demostrar el concepto con un simple pero a la vez inofencivo ejemplo.

Tenemos una clase `Database` que requiere un adaptador para comunicarse con la base de datos. 
Instanciamos el adaptador en el constructor y creamos una dependencia rígida.
Esto dificulta las pruebas y significa que la clase `Database`
esta fuertemente acoplada al adaptador.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Este código se puede refactorizar para usar Inyección de Dependencia y de esta manera desacoplamos la dependencia.
Aquí, inyectamos la dependencia en un constructor haciendo uso de la [promoción de propiedades en el constructor][php-constructor-promotion]
y de esta manera estará disponible como una propiedad de la clase:

{% highlight php %}
<?php
namespace Database;

class Database
{
    public function __construct(protected MySqlAdapter $adapter)
    {
    }
}

class MysqlAdapter {}
{% endhighlight %}

Ahora le estamos dando a la clase `Database` su dependencia en lugar de crearla directamente.
Incluso podríamos crear un método que acepte un argumento de la dependencia y configurarla
de esa manera, o si la propiedad `$adapter` fuera `public` podríamos configurarla directamente.

[php-constructor-promotion]: https://www.php.net/manual/en/language.oop5.decon.php#language.oop5.decon.constructor.promotion
