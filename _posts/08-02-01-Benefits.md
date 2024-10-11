---
title:   Beneficios
isChild: true
anchor:  beneficios_de_las_plantillas
---

## Beneficios {#beneficios_de_las_plantillas_title}

El principal beneficio de utilizar plantillas es la clara separación que crean entre la lógica de presentación y el
resto de tu aplicación. Las plantillas tienen la única responsabilidad de mostrar contenido formateado. No son responsables
de la búsqueda de datos, la persistencia u otras tareas más complejas. Esto lleva a un código más limpio y más legible,
lo cual es especialmente útil en un entorno de equipo donde los desarrolladores trabajan en el código del lado del servidor
(controladores, modelos) y los diseñadores trabajan en el código del lado del cliente (maquetado).

Las plantillas también mejoran la organización del código de presentación. Por lo general, las plantillas se colocan
en una carpeta de "vistas" (_"views"_), cada una definida en un solo archivo. Este enfoque fomenta la reutilización
del código, donde bloques más grandes de código se dividen en piezas más pequeñas y reutilizables, a menudo llamadas
parciales (_partials_). Por ejemplo, el encabezado y el pie de página de tu sitio pueden definirse como plantillas,
las cuales se incluyen antes y después de cada plantilla de página.

Finalmente, dependiendo de la biblioteca que uses, las plantillas pueden ofrecer más seguridad al escapar automáticamente
el contenido generado por los usuarios. Algunas bibliotecas incluso ofrecen un sistema de "sand-boxing", donde los diseñadores
de plantillas solo tienen acceso a variables y funciones en una lista blanca.
