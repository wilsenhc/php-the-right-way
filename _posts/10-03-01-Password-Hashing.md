---
title:   Hashing de Contraseñas
isChild: true
anchor:  hashing_contrasenas
---

## Hashing de Contraseñas {#hashing_contrasenas_title}

Al final, todo el mundo crea una aplicación PHP que depende del inicio de sesión del usuario. Los nombres de usuario
y las contraseñas se almacenan en una base de datos y luego se utilizan para autenticar a los usuarios al iniciar sesión.

Es importante hacer [_hash_][3] correctamente a las contraseñas antes de almacenarlas.
Hacer un hash y cifrar son [dos cosas muy diferentes][7] que a menudo se confunden.

El hashing es una función irreversible y unidireccional. Produce una cadena de longitud fija que no se puede invertir.
Esto significa que se puede comparar un hash con otro para determinar si ambos proceden de la misma cadena de origen,
pero no se puede determinar la cadena original a partir del hash. Si las contraseñas no tienen hash y un tercero no autorizado
accede a la base de datos, todas las cuentas de usuario estarán en peligro.

A diferencia del hashing, el cifrado es reversible (siempre que se tenga la clave). El cifrado es útil en otros ámbitos,
pero es una mala estrategia para almacenar contraseñas de forma segura.

Las contraseñas también deben ser [_salados_][5] (del inglés "salted") individualmente, añadiendo una cadena aleatoria
a cada contraseña antes de aplicar el hash. Así se evitan los ataques de diccionario y el uso de "tablas arco iris"
(una lista inversa de hashes criptográficos para contraseñas comunes).

El hashing y el salting son vitales, ya que a menudo los usuarios utilizan la misma contraseña para varios servicios y la calidad de las contraseñas puede ser deficiente.

Además, debe utilizar [un algoritmo especializado de _password hashing_][6] en lugar de una función hash criptográfica rápida
de uso general (por ejemplo, SHA256). La lista corta de algoritmos hash de contraseña aceptables (a junio de 2018) para usar son:

* Argon2 (disponible en PHP 7.2 y posteriores)
* Scrypt
* **Bcrypt** (PHP se lo proporciona; véase más abajo)
* PBKDF2 con HMAC-SHA256 o HMAC-SHA512

Afortunadamente, hoy en día PHP facilita esta tarea.

**Hashear contraseñas con `password_hash`**

En PHP 5.5 se introdujo `password_hash()`. En este momento usa BCrypt, el algoritmo más fuerte actualmente soportado por PHP.
Sin embargo, será actualizado en el futuro para soportar más algoritmos según sea necesario.
La librería `password_compat` fue creada para proporcionar compatibilidad con PHP >= 5.3.7.

A continuación, hacemos un hash de una cadena y lo comparamos con una nueva cadena. Debido a que nuestras dos cadenas de origen son diferentes ('secret-password' vs. 'bad-password') este login fallará.

{% highlight php %}
<?php
require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    // Contraseña correcta
} else {
    // Contraseña inválida
}
{% endhighlight %}

`password_hash()` se encarga del salado de contraseñas por ti. La sal se almacena, junto con el algoritmo y el "coste", como parte del hash.
`password_verify()` extrae esto para determinar cómo comprobar la contraseña, por lo que no necesitas un campo de base de datos separado para almacenar tus sales.

* [Más información sobre `password_hash()`.] [1]
* [`password_compat` para PHP >= 5.3.7 && < 5.5] [2]
* [Aprenda sobre hashing en relación con la criptografía] [3]
* [Más información sobre las sales] [5]
* [PHP `password_hash()` RFC] [4]


[1]: https://www.php.net/function.password-hash
[2]: https://github.com/ircmaxell/password_compat
[3]: https://wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
[5]: https://wikipedia.org/wiki/Salt_(cryptography)
[6]: https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016
[7]: https://paragonie.com/blog/2015/08/you-wouldnt-base64-a-password-cryptography-decoded
