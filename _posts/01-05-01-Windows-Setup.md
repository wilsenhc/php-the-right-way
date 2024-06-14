---
title:   Instalación en Windows
isChild: true
anchor:  instalacion_en_windows
---

## Instalación en Windows {#instalacion_en_windows_title}

Puede descargar los binarios en [windows.php.net/download][php-downloads]. Después de la extracción de PHP, se recomienda establecer el [PATH][windows-path] a la raíz de su carpeta PHP (donde se encuentra php.exe) para que pueda ejecutar PHP desde cualquier lugar.

Para el aprendizaje y el desarrollo local, puede utilizar el construido en el servidor web con PHP 5.4 + por lo que no necesita preocuparse de
configurarlo. Si desea una solución "todo-en-uno" que incluya un servidor web completo y MySQL también entonces herramientas como
como [XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] y [WAMP][wamp] le ayudará a poner en marcha rápidamente
un entorno de desarrollo Windows. Dicho esto, estas herramientas serán un poco diferentes de las de producción,
así que ten cuidado con las diferencias de entorno si estás trabajando en Windows y desplegando en Linux.

Si necesita ejecutar su sistema de producción en Windows, IIS7 le proporcionará la mayor estabilidad y el mejor rendimiento. Puedes
usar [phpmanager][phpmanager] (un plugin GUI para IIS7) para que la configuración y gestión de PHP sea más sencilla. IIS7 viene con FastCGI
integrado y listo para usar, sólo necesitas configurar PHP como manejador. Para soporte y recursos adicionales existe
un [área dedicada en iis.net][php-iis] para PHP.

Por lo general, la ejecución de su aplicación en diferentes entornos en el desarrollo y la producción puede dar lugar a errores extraños que aparecen cuando usted va a producción. Si estás desarrollando en Windows y desplegando en Linux (o en cualquier otro sistema que no sea Windows) entonces deberías considerar el uso de una [Máquina Virtual](/#virtualizaciones_title).

Chris Tankersley tiene una entrada de blog muy útil sobre qué herramientas utiliza para hacer [desarrollo PHP usando Windows][windows-tools].

[easyphp]: https://www.easyphp.org/
[phpmanager]: http://phpmanager.codeplex.com/
[openserver]: https://ospanel.io/
[wamp]: https://www.wampserver.com/en/
[php-downloads]: https://windows.php.net/download/
[php-iis]: https://php.iis.net/
[windows-path]: https://www.windows-commandline.com/set-path-command-line/
[windows-tools]: https://ctankersley.com/2016/11/13/developing-on-windows-2016/
[xampp]: https://www.apachefriends.org/
