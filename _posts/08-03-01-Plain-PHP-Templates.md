---
title:   Plantillas en PHP simple
isChild: true
anchor:  plantillas_php_simple
---

## Plantillas en PHP simple {#plantillas_php_simple_title}

Las plantillas en PHP simple son simplemente plantillas que utilizan código PHP nativo. Son una opción natural ya que PHP es,
de hecho, un lenguaje de plantillas. Esto significa que puedes combinar código PHP con otro código, como HTML.
Esto es beneficioso para los desarrolladores de PHP ya que no hay nueva sintaxis que aprender, conocen las funciones disponibles
y sus editores de código ya tienen resaltado de sintaxis y autocompletado incorporado. Además, las plantillas en PHP simple tienden
a ser muy rápidas, ya que no se requiere una etapa de compilación.

Todos los frameworks modernos de PHP emplean algún tipo de sistema de plantillas, la mayoría de los cuales utilizan PHP simple por defecto.
Fuera de los frameworks, bibliotecas como [Plates][plates] o [Aura.View][aura] facilitan el trabajo con plantillas en PHP simple al ofrecer
funcionalidades modernas de plantillas, como herencia, layouts y extensiones.

### Ejemplo simple de una plantilla en PHP simple

Usando la biblioteca [Plates][plates].

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
{% endhighlight %}

### Ejemplo de plantilla en PHP simple usando herencia

Haciendo uso de la biblioteca [Plates][plates].

{% highlight php %}
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
{% endhighlight %}

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>
{% endhighlight %}


[plates]: https://platesphp.com/
[aura]: https://github.com/auraphp/Aura.View
