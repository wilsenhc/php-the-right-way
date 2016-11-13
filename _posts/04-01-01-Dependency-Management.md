---
title: Gestión de Dependencias
anchor: gestion-de-dependencias
---

# Gestión de Dependencias {#gestion-de-dependencias}

Existen un sinnúmero de librerías, entorno de trabajo (*frameworks*) y componentes de PHP de donde escoger y lo más probable es que tu proyecto utilice varios de ellos. A esto se les llama dependencias de proyecto. Hasta muy recientemente, PHP no tenía una manera fácil de gestionar tales dependencias. Aun si te hacías cargo de estas manualmente, todavía tendrías que mantenerte al tanto de los cargadores automáticos (autoloaders). Ahora ya no es así.

Actualmente hay dos sistemas principales de gestión de paquetes para PHP: Composer y PEAR. ¿Cuál es el adecuado para ti? La respuesta es, ambos.

* Utiliza **Composer** cuando manejes las dependencias de un solo proyecto.

* Utiliza **PEAR** cuando manejes las dependencias de todo el sistema de PHP en su plataforma.

Generalmente, los paquetes de Composer solo estarán disponibles en los proyectos que especifiques explícitamente, mientras que un paquete de PEAR estaría disponible a todos los proyectos bajo el sistema PHP. Puede que PEAR parezca la propuesta más accesible a primera vista, sin embargo, también existen ventajas al manejar las dependencias con Composer en base al proyecto en que se está trabajando.
