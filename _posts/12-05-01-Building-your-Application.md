---
title:   Construir y Desplegar su Aplicación
isChild: true
anchor:  construir_y_desplegar_su_aplicacion
---

## Construir y Desplegar su Aplicación {#construir_y_desplegar_su_aplicacion_title}

Si te encuentras haciendo cambios manuales en el esquema de la base de datos o ejecutando tus pruebas manualmente antes
de actualizar tus archivos (manualmente), ¡piénsalo dos veces! Con cada tarea manual adicional necesaria para desplegar
una nueva versión de tu aplicación, las posibilidades de cometer errores potencialmente fatales aumentan. Ya sea que estés
lidiando con una actualización simple, un proceso de compilación más complejo o incluso una estrategia de integración continua,
la [automatización][buildautomation] es tu aliada.

Estas son las tareas que podrías querer automatizar:

* Gestión de dependencias
* Compilación y minificación de tus assets
* Ejecución de pruebas
* Creación de documentación
* Empaquetado
* Despliegue


### Herramientas de Despliegue

Las herramientas de despliegue se pueden describir como una colección de scripts que llevan a cabo tareas comunes de despliegue de software. La herramienta de despliegue no es parte de tu software, actúa sobre tu software desde 'afuera'.

Existen muchas herramientas de código abierto disponibles para ayudarte con la automatización de compilación y despliegue, algunas están escritas en PHP y otras no. Esto no debería impedirte usarlas si son más adecuadas para ese trabajo específico. Aquí tienes algunos ejemplos:

[Phing] puede controlar tu proceso de empaquetado, despliegue o pruebas desde un archivo XML. Phing (basado en [Apache Ant]) proporciona un conjunto completo de tareas que usualmente se necesitan para instalar o actualizar una aplicación web y se puede extender con tareas personalizadas adicionales, escritas en PHP. Es una herramienta sólida y robusta que ha estado presente durante mucho tiempo, sin embargo, podría percibirse como una herramienta un poco anticuada debido a la forma en que maneja la configuración (archivos XML).

[Capistrano] es un sistema *para programadores intermedios a avanzados* que permite ejecutar comandos de manera estructurada y repetible en una o más máquinas remotas. Está preconfigurado para desplegar aplicaciones Ruby on Rails, sin embargo, también puedes desplegar sistemas PHP sin problemas. El uso exitoso de Capistrano depende de un conocimiento práctico de Ruby y Rake.

[Ansistrano] es un grupo de roles de Ansible para gestionar fácilmente el proceso de despliegue (despliegue y reversión) de aplicaciones de scripting como PHP, Python y Ruby. Es un port de Ansible para [Capistrano]. Ya ha sido utilizado por muchas empresas de PHP.

[Deployer] es una herramienta de despliegue escrita en PHP. Es simple y funcional. Sus características incluyen ejecución de tareas en paralelo, despliegue atómico y mantener de la consistencia entre servidores. Dispone recetas de tareas comunes para Symfony, Laravel, Zend Framework y Yii. El artículo de Younes Rafie, [Despliegue Fácil de Aplicaciones PHP con Deployer][phpdeploy_deployer], es un gran tutorial para desplegar tu aplicación con esta herramienta.

[Magallanes] es otra herramienta escrita en PHP, con una configuración sencilla con archivos YAML. Soporta múltiples servidores y entornos, despliegue atómico, y tiene algunas tareas integradas que puedes utilizar para herramientas y frameworks comunes.

#### Lectura adicional:

* [Automate your project with Apache Ant][apache_ant_tutorial]
* [Deploying PHP Applications][deploying_php_applications] - libro de pago sobre las mejores prácticas y herramientas para el despliegue de PHP.

### Aprovisionamiento de Servidor

Gestionar y configurar servidores puede ser una tarea abrumadora cuando se esta trabajando con muchos servidores. Existen herramientas para lidiar con esto, que te permiten automatizar tu infraestructura y asegurarte de que tienes los servidores correctos y que están configurados apropiadamente. A menudo, se integran con los principales proveedores de alojamiento en la nube (Amazon Web Services, Heroku, DigitalOcean, etc.) para gestionar instancias, lo que facilita mucho la escalabilidad de una aplicación.

[Ansible] es una herramienta que gestiona tu infraestructura a través de archivos YAML. Es fácil para comenzar a usar y puede gestionar aplicaciones complejas y a gran escala. Hay una API para gestionar instancias en la nube y puede administrarlas a través de un inventario dinámico utilizando ciertas herramientas.

[Puppet] es una herramienta que tiene su propio lenguaje y tipos de archivos para gestionar servidores y configuraciones. Se puede usar en una configuración maestro/cliente o en un modo "sin maestro". En el modo maestro/cliente, los clientes consultan al maestro(s) central(es) para obtener nuevas configuraciones a intervalos establecidos y se actualizan si es necesario. En el modo sin maestro, puedes enviar cambios a tus nodos.

[Chef] es un potente marco de integración de sistemas basado en Ruby que puedes utilizar para construir todo tu entorno de servidor o máquinas virtuales. Se integra bien con Amazon Web Services a través de su servicio llamado OpsWorks.

#### Lectura adicional:

* [An Ansible Tutorial][an_ansible_tutorial]
* [Ansible for DevOps][ansible_for_devops] - libro de pago sobre todo lo relacionado con Ansible.
* [Ansible for AWS][ansible_for_aws] - libro de pago sobre la integración de Ansible y Amazon Web Services
* [Three part blog series about deploying a LAMP application with Chef, Vagrant, and EC2][chef_vagrant_and_ec2]
* [Chef Cookbook which installs and configures PHP and the PEAR package management system][Chef_cookbook]
* [Chef video tutorial series][Chef_tutorial]

### Integración Continua

> La Integración Continua es una práctica de desarrollo de software en la que los miembros de un equipo integran su trabajo con frecuencia, generalmente cada persona integra al menos una vez al día, lo que conduce a múltiples integraciones por día. Muchos equipos descubren que este enfoque reduce significativamente los problemas de integración y permite desarrollar software cohesivo de manera más rápida.

*-- Martin Fowler*

Existen diferentes maneras de implementar la integración continua para PHP. [Travis CI] ha hecho un gran trabajo al hacer que la integración continua sea una realidad incluso para proyectos pequeños. Travis CI es un servicio de integración continua hospedado. Se puede integrar con GitHub y ofrece soporte para muchos lenguajes, incluido PHP. GitHub tiene flujos de trabajo de integración continua con [GitHub Actions][github_actions].

#### Lectura adicional:

* [Integración Continua con Jenkins][Jenkins]
* [Integración Continua con PHPCI][PHPCI]
* [Integración Continua con PHP Censor][PHP Censor]
* [Integración Continua con Teamcity][Teamcity]

[buildautomation]: https://wikipedia.org/wiki/Build_automation
[Phing]: https://www.phing.info/
[Apache Ant]: https://ant.apache.org/
[Capistrano]: https://capistranorb.com/
[Ansistrano]: https://ansistrano.com
[phpdeploy_deployer]: https://www.sitepoint.com/deploying-php-applications-with-deployer/
[Chef]: https://www.chef.io/
[chef_vagrant_and_ec2]: https://web.archive.org/web/20190307220000/http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/sous-chefs/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PL11cZfNdwNyNYcpntVe6js-prb80LBZuc
[apache_ant_tutorial]: https://code.tutsplus.com/tutorials/automate-your-projects-with-apache-ant--net-18595
[Travis CI]: https://www.travis-ci.com/
[Jenkins]: https://jenkins.io/
[PHPCI]: https://github.com/dancryer/phpci
[PHP Censor]: https://github.com/php-censor/php-censor
[Teamcity]: https://www.jetbrains.com/teamcity/
[Deployer]: https://deployer.org/
[Magallanes]: https://www.magephp.com/
[deploying_php_applications]: https://deployingphpapplications.com/
[Ansible]: https://www.ansible.com/
[Puppet]: https://puppet.com/
[ansible_for_devops]: https://leanpub.com/ansible-for-devops
[ansible_for_aws]: https://leanpub.com/ansible-for-aws
[an_ansible_tutorial]: https://serversforhackers.com/an-ansible-tutorial
[github_actions]: https://docs.github.com/en/actions
