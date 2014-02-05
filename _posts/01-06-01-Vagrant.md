---
title: Vagrant
isChild: true
---

## Vagrant

Si ejecuta su aplicación en diferentes entornos para desarrollo y producción puede conducir a que se manifiesten errores extraños al usar su aplicación. También es complicado mantener los diferentes entornos de desarrollo actualizados con la misma versión para todas las librerías utilizadas cuando se trabaja con un equipo de desarrollo.

Si está desarrollando en Windows y desplegando en Linux (o cualquier otro sistema que no sea Windows) considere el uso de una Máquina Virtual. Quizás suene un poco complicado, pero con el uso de [Vagrant][vagrant] puede configurar una máquina virtual en pocos pasos. Estas máquinas virtuales (box) pueden ser configuradas manualmente, o puede utilizar un software "suministrador" como [Puppet][puppet] o [Chef][chef] para hacer esto por usted. La suministración de una box base es una forma genial de asegurarse que las múltiples máquinas virtuales estén configuradas en forma idéntica y le evitan la necesidad de mantener una complicada lista de comandos de "configuración". También puede "destruir" su box base y re-crearla sin muchos pasos manuales, por lo que es fácil crear una instalación "fresca".

Vagrant crea carpetas compartidas para compartir su código entre su equipo y su máquina virtual, lo que significa que puede crear y editar sus archivos en su equipo y después correr el código dentro de su máquina virtual.

### Un poco de ayuda

Si necesita un poco de ayuda para comenzar a utilizar Vagrant aquí hay dos servicios que pueden serle útiles:

- [Rove][rove]: servicio que le permite pre-generar una configuración Vagrant típica, siendo PHP una de las opciones. El suministro es realizado con Chef.
- [Puphpet][puphpet]: simple GUI para configurar maquinas virtuales para desarrollos en PHP. **Muy enfocado a PHP**. Además de las máquinas virtuales locales, puede ser utilizado para desarrollos en la nube. El aprovisionamiento esta realizado con Puppet.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/