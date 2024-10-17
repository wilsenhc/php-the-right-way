---
title:   Seguridad de Aplicaciones Web
isChild: true
anchor:  seguridad_de_aplicaciones_web
---

## Seguridad de Aplicaciones Web {#seguridad_de_aplicaciones_web_title}

Es muy importante que todo desarrollador PHP aprenda [los fundamentos de la seguridad de las aplicaciones web][4], que pueden dividirse en un puñado de temas generales:

1. Separación de código y datos.
   * Cuando los datos se ejecutan como código, se obtiene Inyección SQL, Cross-Site Scripting, Inclusión de Archivos Locales/Remotos, etc.
   * Cuando el código se imprime como datos, se producen fugas de información (revelación del código fuente o, en el caso de los programas en C,
     información suficiente para saltarse [ASLR][5]).
2. Lógica de aplicación.
   * Ausencia de controles de autenticación o autorización.
   * Validación de las entradas.
3. Entorno operativo.
   * Versiones de PHP.
   * Bibliotecas de terceros.
   * Sistema operativo.
4. Puntos débiles de la criptografía.
   * [Números aleatorios débiles][6].
   * [Ataques con texto cifrado elegido][7].
   * [Fugas de información por canales laterales][8].

Hay gente mala lista y dispuesta a explotar su aplicación web. Es importante que tome las precauciones necesarias
para reforzar la seguridad de su aplicación web. Por suerte, la buena gente de [The Open Web Application Security Project][1] (OWASP)
ha recopilado una lista exhaustiva de problemas de seguridad conocidos y métodos para protegerse contra ellos. Se trata de una lectura
obligatoria para los desarrolladores preocupados por la seguridad. [Survive The Deep End: PHP Security][3] de Padraic Brady es también
otra buena guía de seguridad de aplicaciones web para PHP.

* [Lea la Guía de seguridad de OWASP][2]


[1]: https://www.owasp.org/
[2]: https://www.owasp.org/index.php/Guide_Table_of_Contents
[3]: https://phpsecurity.readthedocs.io/en/latest/index.html
[4]: https://paragonie.com/blog/2015/08/gentle-introduction-application-security
[5]: https://www.techtarget.com/searchsecurity/definition/address-space-layout-randomization-ASLR
[6]: https://paragonie.com/blog/2016/01/on-design-and-implementation-stealth-backdoor-for-web-applications
[7]: https://paragonie.com/blog/2015/05/using-encryption-and-authentication-correctly
[8]: https://blog.ircmaxell.com/2014/11/its-all-about-time.html
