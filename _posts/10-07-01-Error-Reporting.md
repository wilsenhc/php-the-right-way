---
title:   Reporte de Errores
isChild: true
anchor:  reporte_de_errores
---

## Reporte de Errores {#reporte_de_errores_title}

El registro de errores puede ser útil para encontrar los puntos problemáticos en su aplicación, pero también puede exponer
información sobre la estructura de su aplicación al mundo exterior. Para proteger eficazmente su aplicación de los problemas
que podrían ser causados por la salida de estos mensajes, es necesario configurar el servidor de manera
diferente en el desarrollo frente a la producción (en vivo).

### Desarrollo

Para mostrar todos los errores posibles durante el **desarrollo**, configure los siguientes parámetros en su `php.ini`:

{% highlight ini %}
display_errors = On
display_startup_errors = On
error_reporting = -1
log_errors = On
{% endhighlight %}

> Pasando el valor `-1` se mostrarán todos los errores posibles, incluso cuando se añadan nuevos niveles y constantes en futuras
> versiones de PHP. La constante `E_ALL` también se comporta de esta manera a partir de PHP 5.4. -
> [php.net](https://www.php.net/function.error-reporting)

La constante de nivel de error `E_STRICT` se introdujo en 5.3.0 y no forma parte de `E_ALL`, sin embargo pasó a
formar parte de `E_ALL` en 5.4.0. ¿Qué significa esto? En términos de informar de todos los errores posibles en la versión 5.3
significa que debe utilizar `-1` o `E_ALL | E_STRICT`.

**Informar de todos los errores posibles por versión de PHP**

* &lt; 5.3 `-1` o `E_ALL`
* &nbsp; 5.3 `-1` o `E_ALL | E_STRICT`
* &gt; 5.3 `-1` o `E_ALL`

### Producción

Para ocultar los errores en su entorno de **producción**, configure su `php.ini` así:

{% highlight ini %}
display_errors = Off
display_startup_errors = Off
error_reporting = E_ALL
log_errors = On
{% endhighlight %}

Con esta configuración en producción, los errores seguirán registrándose en los registros de errores del servidor web,
pero no se mostrarán al usuario. Para más información sobre estos ajustes, consulte el manual de PHP:

* [error_reporting](https://www.php.net/errorfunc.configuration#ini.error-reporting)
* [display_errors](https://www.php.net/errorfunc.configuration#ini.display-errors)
* [display_startup_errors](https://www.php.net/errorfunc.configuration#ini.display-startup-errors)
* [log_errors](https://www.php.net/errorfunc.configuration#ini.log-errors)
