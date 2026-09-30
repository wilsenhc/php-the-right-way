---
title:   Instalación en Windows
isChild: true
anchor:  instalacion_en_windows
---

## Instalación en Windows {#instalacion_en_windows_title}

Puedes descargar los binarios desde [la página de descargas de php.net][php-downloads]. Después de la extracción de PHP, se 
recomienda establecer el [PATH][windows-path] a la raíz de tu carpeta PHP (donde se encuentra php.exe) para que puedas ejecutar
PHP desde cualquier lugar.

Para el aprendizaje y el desarrollo local, puedes utilizar el [servidor web integrado](/#builtin_web_server_title) con PHP 5.4+ por lo
que no necesitas preocuparte por configurarlo. Si deseas una solución "todo-en-uno" que incluya un servidor web completo
y MySQL también, herramientas como [EasyPHP][easyphp], [OpenServer][openserver] o [WampServer][wamp] te ayudarán a poner en 
marcha un entorno de desarrollo de Windows rápidamente. Dicho esto, estas herramientas serán un poco diferentes del 
entorno de producción, así que ten cuidado con las diferencias de entorno si trabajas en Windows y despliegas en Linux.

Por lo general, ejecutar tu aplicación en un entorno diferente entre desarrollo y producción puede dar lugar a errores extraños 
que aparecen al pasar a producción. Si desarrollas en Windows y despliegas en Linux (o en cualquier otro sistema que no sea Windows), entonces
deberías considerar el uso de una [Máquina Virtual](/#virtualization_title) o el [Subsistema de Windows para Linux (WSL)][wsl].

Chris Tankersley tiene una entrada de blog muy útil sobre qué herramientas utiliza para hacer [desarrollo PHP usando Windows][windows-tools].

[easyphp]: https://www.easyphp.org/
[openserver]: https://ospanel.io/en/
[php-downloads]: https://www.php.net/downloads.php?os=windows
[wamp]: https://wampserver.aviatechno.net/?lang=en
[windows-path]: https://www.windows-commandline.com/set-path-command-line/
[windows-tools]: https://ctankersley.com/2016/11/13/developing-on-windows-2016/
[wsl]: https://learn.microsoft.com/en-us/windows/wsl/
