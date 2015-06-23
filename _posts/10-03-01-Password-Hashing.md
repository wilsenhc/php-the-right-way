---
anchor: password-hashing
isChild: true
---

## Hash de contraseñas


Con el tiempo todo el mundo desarrolla una aplicación PHP que se apoya en la conexión del usuario. Los nombres de usuario y las contraseñas se almacenan en una base de datos y posteriormente son utilizados para autenticar a los usuarios en el login.

Es importante que usted [realice hash](https://es.wikipedia.org/wiki/Funci%C3%B3n_hash_criptogr%C3%A1fica) de las contraseñas correctamente antes de almacenarlos. Una vez realizado el hash a la contraseña con una función aplicada contra la contraseña del usuario, el paso es irreversible. Esto produce una cadena de longitud fija que no puede ser revertida factiblemente. Esto significa que puede comparar un hash contra otro para determinar si ambos proceden de la misma cadena de origen, pero no se puede determinar la cadena original. Si las contraseñas no están hasheadas y se accede a la base de datos por un tercero no autorizado, todas las cuentas de usuario están comprometidas. Algunos usuarios pueden (por desgracia) utilizar la misma contraseña para otros servicios. Por lo tanto, es importante tomar en serio la seguridad.

**Hash de contraseñas con `password_hash`**

En PHP 5.5 fue introducido `password_hash`. En este momento está usando BCrypt, el algoritmo más fuerte actualmente soportado por PHP. Se actualizará en el futuro para apoyar a más algoritmos, según sea necesario. La librería `password_compat` fue creada para proveer compatibilidad a las versiones PHP >= 5.3.7.

Más abajo hacemos hash a una cadena de texto, y seguidamente comprobamos el hash con una nueva cadena. Debido a que las fuentes de nuestras dos cadenas son distintas ('contraseña-secreta' vs 'mala-contraseña') el login fallará.

{% highlight php %}
<?php

require 'password.php';

$passwordHash = password_hash('contraseña-secreta', PASSWORD_DEFAULT);

if (password_verify('mala-contraseña', $passwordHash)) {
    // Contraseña correcta
} else {
    // Contraseña incorrecta
}
{% endhighlight %}



* [Aprende más acerca de `password_hash`] [1]
* [`password_compat` para PHP  >= 5.3.7 && < 5.5] [2]
* [Obtener información acerca de hashing en cuanto a la criptografía] [3]
* [PHP `password_hash` RFC] [4]

[1]: http://es.php.net/manual/es/function.password-hash.php
[2]: https://github.com/ircmaxell/password_compat
[3]: https://es.wikipedia.org/wiki/Funci%C3%B3n_hash_criptogr%C3%A1fica
[4]: https://wiki.php.net/rfc/password_hash
