---
title: Configuración en Windows
anchor: configuracion-windows
isChild: true
---

## Configuración en Windows {#configuracion-windows}

Hay un sinnúmero de maneras de configurar PHP en el sistema Windows. Usted puede [descargar los binarios](php-downloads) y recientemente el paquete de instalación estaba disponible en el formato '.msi'. Este paquete de instalación ya no se actualiza y la última versión fue PHP 5.3.0.

Para aprender PHP o el desarrollo local, se puede utilizar el servidor web embebido que viene con la versión PHP 5.4, así no tendrá que preocuparse por configurar un servidor por separado. Ahora bien, si le gustaría disponer de una solución tipo “todo incluido”, que le ofrece un servidor web completo junto con el gestor de base de datos MySQL, entonces herramientas como el [Web Platform Installer][wpi], [XAMPP][xampp] y [WAMP][wamp] le ayudaran a configurar un entorno de desarrollo web en Windows más fácilmente y en menos tiempo. Tenga en consideración que estas herramientas son un poco diferentes a las que usara en su sistema de producción, así que tenga cuidado de las diferencias en el entorno de su aplicación si es que la desarrolla en Windows pero la despliega en Linux.

Si necesita correr un sistema de producción en Windows entonces el servidor IIS 7 le ofrecerá un entorno más estable y con el mejor rendimiento.  Una herramienta como [phpmanager][phpmanager] (un complemento GUI para IIS 7) le simplificara la gestión y configuración de PHP en este servidor. IIS 7 viene configurado con FastCGI listo para su uso, solo necesita apuntar a PHP como controlador. Para más información y recursos adicionales refiérase a la [área dedicada en iis.net][php-iis] para PHP.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/