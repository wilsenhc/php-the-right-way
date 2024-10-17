---
title:   Filtrado de Datos
isChild: true
anchor:  filtrado_de_datos
---

## Filtrado de Datos {#filtrado_de_datos_title}

Nuca (nunca) confíes en la introducción de datos ajenos en tu código PHP. Siempre sanee y valide la entrada ajena antes
de usarla en el código. Las funciones `filter_var()` y `filter_input()` pueden sanear texto y validar formatos de texto
(por ejemplo, direcciones de correo electrónico).

La entrada ajena puede ser cualquier cosa: datos de formulario `$_GET` y `$_POST`, algunos valores en el superglobal `$_SERVER`,
y el cuerpo de la petición HTTP a través de `fopen('php://input', 'r')`. Recuerde, la entrada de datos externos
no se limita a los datos del formulario enviados por el usuario. Los archivos cargados y descargados, los valores de sesión,
los datos de cookies y los datos de servicios web de terceros también son entradas de datos externos.

Aunque la introducción de datos ajenos pueden almacenarse, combinarse y accederse posteriormente, siguen siendo entrada ajena.
Cada vez que proceses, des salida, concatenes o incluyas datos en tu código, pregúntate si los datos están filtrados correctamente
y si son de confianza.

Los datos pueden _filtrarse_ de forma diferente en función de su finalidad. Por ejemplo, cuando una entrada ajena no filtrada
se pasa a la salida de una página HTML, ¡puede ejecutar HTML y JavaScript en su sitio! Esto se conoce como Cross-Site Scripting (XSS)
y puede ser un ataque muy peligroso. Una forma de evitar XSS es desinfectar todos los datos generados por el usuario antes de enviarlos
a la página eliminando las etiquetas HTML con la función `strip_tags()` o escapando caracteres con significado especial
en sus respectivas entidades HTML con las funciones `htmlentities()` o `htmlspecialchars()`.

Otro ejemplo es pasar opciones para ser ejecutadas en la línea de comandos. Esto puede ser extremadamente peligroso (y suele ser una mala idea),
pero puede utilizar la función integrada `escapeshellarg()` para desinfectar los argumentos del comando ejecutado.

Un último ejemplo es aceptar una entrada extraña para determinar un fichero a cargar del sistema de ficheros. Esto puede
ser explotado cambiando el nombre del archivo a una ruta de archivo. Es necesario eliminar `"/"`, `"../"`,
[bytes nulos][6], u otros caracteres de la ruta del archivo para que no pueda cargar archivos ocultos, no públicos o sensibles.

* [Más información sobre el filtrado de datos][1]
* [Más información sobre `filter_var`][4]
* [Más información sobre `filter_input`][5]
* [Más información sobre la gestión de bytes nulos][6]

### Sanitization

La sanitización elimina (o escapa) caracteres ilegales o inseguros de los datos de entrada ajenos.

Por ejemplo, debe desinfectar los datos de entrada ajenos antes de incluirla en HTML o insertarla en una consulta SQL sin procesar.
Cuando use parámetros vinculados con [PDO](#bases_de_datos), se limpiarán los datos de entrada por usted.

A veces es necesario permitir algunas etiquetas HTML seguras en los datos de entrada al incluirla en la página HTML.
Esto es muy difícil de hacer y muchos lo evitan usando otros formatos más restringidos como Markdown o BBCode, aunque para ello
existen librerías de filtrado de datos como [HTML Purifier][html-purifier].

[Ver Filtros de Sanitización][2]

### Deserialización

Es peligroso deserializar datos de usuarios u otras fuentes no confiables utilizando `unserialize()`.
Hacerlo puede permitir a usuarios maliciosos instanciar objetos (con propiedades definidas por el usuario) cuyos destructores serán ejecutados,
**incluso si los propios objetos no son utilizados**. Por lo tanto, debes evitar deserializar datos que no sean de confianza.

Utiliza un formato de intercambio de datos seguro y estándar como JSON (a través de [`json_decode`][json_decode] y [`json_encode`][json_encode]) si necesitas pasar datos serializados al usuario.

### Validación

La validación garantiza que la entrada de datos ajenos es la esperada. Por ejemplo, es posible que desee validar una dirección de correo electrónico, un número de teléfono o la edad al procesar un envío de registro.

[Ver Filtros de Validación][3]


[1]: https://www.php.net/book.filter
[2]: https://www.php.net/filter.filters.sanitize
[3]: https://www.php.net/filter.filters.validate
[4]: https://www.php.net/function.filter-var
[5]: https://www.php.net/function.filter-input
[6]: https://www.php.net/security.filesystem.nullbytes
[html-purifier]: http://htmlpurifier.org/
[json_decode]: https://www.php.net/manual/function.json-decode.php
[json_encode]: https://www.php.net/manual/function.json-encode.php
