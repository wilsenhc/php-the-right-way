---
anchor: dependency_management
---

# Dependency Management {#dependency_management_title}

There are a ton of PHP libraries, frameworks, and components to choose from. Your project will likely use 
several of them — these are project dependencies. Until recently, PHP did not have a good way to manage
these project dependencies. Even if you managed them manually, you still had to worry about autoloaders.
That is no longer an issue.

Currently there are two major package management systems for PHP - [Composer] and [PEAR]. Composer is currently
the most popular package manager for PHP, however for a long time PEAR was the primary package manager in use.
Knowing PEAR's history is a good idea, since you may still find references to it even if you never use it.

[Composer]: /#composer_and_packagist
[PEAR]: /#pear

* Utiliza **PEAR** cuando manejes las dependencias de todo el sistema de PHP en su plataforma.

Generalmente, los paquetes de Composer solo estarán disponibles en los proyectos que especifiques explícitamente, mientras que un paquete de PEAR estaría disponible a todos los proyectos bajo el sistema PHP. Puede que PEAR parezca la propuesta más accesible a primera vista, sin embargo, también existen ventajas al manejar las dependencias con Composer en base al proyecto en que se está trabajando.
