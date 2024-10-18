---
title:   Servidores Virtuales o Dedicados
isChild: true
anchor:  servidores_virtuales_o_dedicados
---

## Servidores Virtuales o Dedicados {#servidores_virtuales_o_dedicados_title}

Si te sientes cómodo con la administración de sistemas, o estás interesado en aprender, los servidores virtuales o dedicados
te permiten tener control total sobre el entorno de producción de tu aplicación.

### nginx y PHP-FPM

PHP, con el gestor de procesos FastCGI (_FastCGI Process Manager_, FPM por sus siglas en inglés) integrado en PHP,
se complementa muy bien con [nginx], el cual es un servidor web ligero y de alto rendimiento. Utiliza menos memoria que
Apache y puede manejar mejor más solicitudes concurrentes. Esto es especialmente importante en servidores virtuales que no tienen mucha memoria disponible.

* [Leer más sobre nginx][nginx]
* [Leer más sobre PHP-FPM][phpfpm]
* [Leer más sobre configurar nginx y PHP-FPM de forma segura][secure-nginx-phpfpm]

### Apache y PHP

PHP y Apache tienen una larga historia juntos. Apache es ampliamente configurable y cuenta con muchos [módulos][apache-modules] disponibles para extender su funcionalidad. Es una elección común para servidores compartidos y una configuración sencilla para frameworks PHP y aplicaciones de código abierto como WordPress. Desafortunadamente, Apache por defecto utiliza más recursos que nginx y no puede manejar tantos visitantes al mismo tiempo.

Apache posee varias configuraciones posibles para ejecutar PHP. La más común y más fácil de configurar es el [prefork MPM]
con `mod_php`. Aunque no es la más eficiente en términos de memoria, es la más sencilla de hacer funcionar y utilizar.
Probablemente sea la mejor opción si no deseas profundizar demasiado en los aspectos de administración del servidor.
Ten en cuenta que si usas `mod_php` DEBES usar el prefork MPM.

Alternativamente, si quieres sacar más rendimiento y estabilidad de Apache, puedes aprovechar el mismo sistema FPM que
nginx y ejecutar el [worker MPM] o el [event MPM] con `mod_fastcgi` o `mod_fcgid`. Esta configuración será significativamente
más eficiente en memoria y mucho más rápida, pero requiere más trabajo para configurarla.

Si estás ejecutando Apache 2.4 o posterior, puedes usar [mod_proxy_fcgi] para obtener un gran rendimiento y es fácil de configurar.

* [Leer más sobre Apache][apache]
* [Leer más sobre Multi-Processing Modules][apache-MPM]
* [Leer más sobre mod_fastcgi][mod_fastcgi]
* [Leer más sobre mod_fcgid][mod_fcgid]
* [Leer más sobre mod_proxy_fcgi][mod_proxy_fcgi]
* [Leer más sobre setting up Apache and PHP-FPM with mod_proxy_fcgi][tutorial-mod_proxy_fcgi]


[nginx]: https://nginx.org/
[phpfpm]: https://www.php.net/install.fpm
[secure-nginx-phpfpm]: https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/
[apache-modules]: https://httpd.apache.org/docs/2.4/mod/
[prefork MPM]: https://httpd.apache.org/docs/2.4/mod/prefork.html
[worker MPM]: https://httpd.apache.org/docs/2.4/mod/worker.html
[event MPM]: https://httpd.apache.org/docs/2.4/mod/event.html
[apache]: https://httpd.apache.org/
[apache-MPM]: https://httpd.apache.org/docs/2.4/mod/mpm_common.html
[mod_fastcgi]: https://blogs.oracle.com/opal/post/php-fpm-fastcgi-process-manager-with-apache-2
[mod_fcgid]: https://httpd.apache.org/mod_fcgid/
[mod_proxy_fcgi]: https://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html
[tutorial-mod_proxy_fcgi]: https://serversforhackers.com/video/apache-and-php-fpm
