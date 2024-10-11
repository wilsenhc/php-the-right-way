---
title:   Plantillas Compiladas
isChild: true
anchor:  plantillas_compiladas
---

## Plantillas Compiladas {#plantillas_compiladas_title}

Aunque PHP ha evolucionado hasta convertirse en un lenguaje maduro, orientado a objetos, [no ha mejorado mucho][article_templating_engines]
como lenguaje de plantillas. Las plantillas compiladas, como [Twig], [Brainy] o [Smarty]*, llenan este vacío al ofrecer
una nueva sintaxis diseñada específicamente para la creación de plantillas. Desde el escape automático hasta la herencia
y estructuras de control simplificadas, las plantillas compiladas están diseñadas para ser más fáciles de escribir, más
legibles y más seguras de usar. Las plantillas compiladas incluso pueden compartirse entre diferentes lenguajes,
siendo [Mustache] un buen ejemplo de esto. Dado que estas plantillas deben ser compiladas, hay una ligera pérdida de rendimiento,
sin embargo, esto es muy mínimo cuando se utiliza un sistema de caché apropiado.

**Aunque Smarty ofrece escape automático, NO está habilitado por defecto.*

### Ejemplo de una plantilla compilada

Haciendo uso de [Twig].

{% highlight html+jinja %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### Ejemplo de plantillas compiladas usando herencia

Usando [Twig].

{% highlight html+jinja %}
{% raw %}
// template.html

<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
{% endraw %}
{% endhighlight %}

{% highlight html+jinja %}
{% raw %}
// user_profile.html

{% extends "template.html" %}

{% block title %}User Profile{% endblock %}
{% block content %}
    <h1>User Profile</h1>
    <p>Hello, {{ name }}</p>
{% endblock %}
{% endraw %}
{% endhighlight %}


[article_templating_engines]: http://fabien.potencier.org/templating-engines-in-php.html
[Twig]: https://twig.symfony.com/
[Brainy]: https://github.com/box/brainy
[Smarty]: https://www.smarty.net/
[Mustache]: https://mustache.github.io/
