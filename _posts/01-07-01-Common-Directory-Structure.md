---
title:   Estructura Común de Directorios
isChild: true
anchor:  estructura_comun_de_directorios
---

## Estructura Común de Directorios {#estructura_comun_de_directorios_title}

Una pregunta común entre los que empiezan a escribir programas para la web es: "¿dónde pongo mis archivos?". A lo largo de los años, la respuesta ha sido consistentemente "donde está el `DocumentRoot`". Aunque esta respuesta no es del todo completa, es un buen punto de partida.

Por razones de seguridad, los archivos de configuración no deben ser accesibles por los visitantes de un sitio; por lo tanto, los scripts públicos se guardan en un directorio público y las configuraciones y datos privados se guardan fuera de ese directorio.

En cada equipo, CMS o framework en el que uno trabaja, cada uno de ellos utiliza una estructura de directorios estándar. Sin embargo, si uno está empezando un proyecto por si mismo, saber qué estructura de sistema de archivos utilizar puede ser intimidante.

[Paul M. Jones] ha realizado una fantástica investigación sobre las prácticas comunes de decenas de miles de proyectos de github en el ámbito de PHP. Ha compilado una estructura estándar de archivos y directorios, el [Standard PHP Package Skeleton], basado en esta investigación. En esta estructura de directorios, `DocumentRoot` debe apuntar a `public/`, las pruebas unitarias deben estar en el directorio `tests/`, y las librerías de terceros, instaladas por [composer], deben estar en el directorio `vendor/`. Para otros archivos y directorios, seguir el [Standard PHP Package Skeleton] tendrá más sentido para los contribuidores de un proyecto.

[Paul M. Jones]: https://paul-m-jones.com/
[Standard PHP Package Skeleton]: https://github.com/php-pds/skeleton
[Composer]: /#composer_and_packagist
