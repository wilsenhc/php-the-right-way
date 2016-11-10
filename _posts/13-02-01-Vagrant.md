---
isChild: true
anchor: vagrant
---

## Vagrant {#vagrant_title}

[Vagrant][vagrant] te ayuda a construir cajas virtuales (virtual boxes) sobre entornos virtuales conocidos y configurará estos entornos usando un simple archivo de configuración. Estas cajas pueden configurarse manualmente o puedes usar software "aprovisionado" como [Puppet][puppet] o [Chef][chef] para que haga todo el trabajo por ti. Suministrar la base para una caja es una excelente manera de asegurarte de que múltiples cajas serán configuradas de forma idéntica y elimina la necesidad de mantener complicadas listas de comandos de "configuración". También puedes "destruir" una caja base y volver a crearla en unos pocos pasos, lo que facilita la creación de una instalación "nueva".

Vagrant crea carpetas para compartir tu código entre tu host y tu máquina virtual, lo que significa que puedes crear y editar tus archivos en tu máquina host y luego ejecutar el código dentro de tu máquina virtual.

### Una pequeña ayuda

Si necesitas ayuda para empezar a usar Vagrant, estos son algunos servicios que podrían serte muy útiles:

- [Rove][rove]: servicio que te permitirá "pre-generar" builds Vagrant típicos, PHP está entre sus opciones. El "aprovisionamiento" es hecho con Chef.
- [Puphpet][puphpet]: Sencilla interfase gráfica de usuario (GUI por sus siglas en inglés) para configurar máquinas virtuales para desarrollo con PHP. **Fuertemente enfocadas en PHP**. Además de las MVs (máquinas virtuales) locales, Puphept también puede ser usado para hacer despliegues hacia servicios en la nube. El "aprovisionamiento" es hecho con Puppet.
- [Protobox][protobox]: Es una capa en el tope de Vagrant y una interfase web para configurar máquinas virtuales para desarrollo web. Un simple documento YAML controla todo lo que será instalado en la MV.
- [Phansible][phansible]: proporciona una sencilla interfase que te facilita  la generación de Ansible Playbooks para proyectos basados en PHP.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
[phansible]: http://phansible.com/
