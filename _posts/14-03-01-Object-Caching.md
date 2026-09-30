---
title:   Caché de Objetos
isChild: true
anchor:  cache_objetos
---

## Caché de Objetos {#cache_objetos_title}

A veces puede ser beneficioso almacenar en caché objetos individuales en tu código, como en el caso de datos que son costosos de obtener o llamadas a bases de datos donde el resultado es poco probable que cambie. Puedes usar software de almacenamiento en caché de objetos para mantener estos fragmentos de datos en memoria para un acceso extremadamente rápido más adelante. Si guardas estos elementos en un almacén de datos después de recuperarlos, y luego los obtienes directamente desde la caché para las solicitudes siguientes, puedes obtener una mejora significativa en el rendimiento, así como reducir la carga en tus servidores de bases de datos.

Muchas de las soluciones populares de almacenamiento en caché de bytecode también te permiten almacenar datos personalizados, por lo que hay aún más razones para aprovecharlas. APCu y WinCache proporcionan APIs para guardar datos de tu código PHP en su caché de memoria.

Los sistemas de almacenamiento en caché de objetos en memoria más comúnmente utilizados son APCu y memcached. APCu es una excelente opción para el almacenamiento en caché de objetos, incluye una API simple para agregar tus propios datos a su caché de memoria y es muy fácil de configurar y usar. La única limitación real de APCu es que está vinculado al servidor donde está instalado. Memcached, por otro lado, se instala como un servicio separado y se puede acceder a él a través de la red, lo que significa que puedes almacenar objetos en un almacén de datos de alta velocidad en una ubicación central y muchos sistemas diferentes pueden obtenerlos desde allí.

Note that whether the cache is shared across PHP processes depends on how PHP is used. When running PHP via PHP-FPM,
the cache is shared across all processes of all pools. When running PHP as a (Fast-)CGI application inside your
webserver, the cache is not shared, i.e every PHP process will have its own APCu data. When running PHP on the command
line, the cache is not shared and will only exist for the duration of the command, so you have to be mindful of your
situation and goals. You might want to consider using memcached instead, as it's not tied to the PHP processes.

En una configuración en red, APCu generalmente superará a memcached en términos de velocidad de acceso, pero memcached podrá escalar más rápido y en mayor medida. Si no esperas tener varios servidores ejecutando tu aplicación, o no necesitas las características adicionales que ofrece memcached, entonces probablemente APCu sea tu mejor opción para el almacenamiento en caché de objetos.

Ejemplo de lógica usando APCu:

{% highlight php %}
<?php
// check if there is data saved as 'expensive_data' in cache
$data = apcu_fetch('expensive_data');
if ($data === false) {
    // data is not in cache; save result of expensive call for later use
    apcu_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

### Learn more about popular object caching systems:

* [APCu](https://github.com/krakjoe/apcu)
* [APCu Documentation](https://www.php.net/apcu)
* [Memcached](https://memcached.org/)
* [Redis](https://redis.io/)
* [WinCache Functions](https://www.php.net/ref.wincache)
