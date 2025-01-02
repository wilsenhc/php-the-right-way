---
title:   Trabajar con UTF-8
isChild: true
anchor:  php_y_utf8
---

## Trabajar con UTF-8 {#php_y_utf8_title}

_Esta sección fue escrita originalmente por Alex Cabal sobre PHP Best Practices y se ha
utilizado como base para nuestras propias recomendaciones acerca de UTF-8_.

### No existe una forma única. Sea cuidadoso, detallista y consistente.

Ahora mismo, PHP no soporta Unicode a bajo nivel. Hay formas de asegurarse de que las cadenas de texto UTF-8 sean procesadas
correctamente, pero no es sencillo, además requiere que profundizar en todos los niveles de la aplicación web, desde
HTML, pasando por SQL hasta PHP. Nos esforzamos por hacer un breve resumen práctico.

### UTF-8 al nivel de PHP

Las operaciones básicas con cadenas, como la concatenación de dos cadenas o la asignación de cadenas a variables,
no necesitan nada especial de UTF-8. Sin embargo, la mayoría de las funciones para el manejo de cadenas como
`strpos()` o `strlen()`, necesitan consideración especial. A menudo, estas funciones tienen su contraparte con
funciones `mb_*` como por ejemplo: `mb_strpos()` o `mb_strlen()`. Estas funciones `mb_*` están disponibles para usted
vía la extensión para el manejo de [Cadenas de Caracteres Cadenas Multibyte](https://php.net/manual/es/book.mbstring.php),
y están diseñadas específicamente para operar con cadenas Unicode.

Siempre se debe utilizar las funciones `mb_*` para trabajar con cadenas Unicode. Por ejemplo, si usa `substr()` sobre
una cadena UTF-8, hay una gran posibilidad de que el resultado incluya algunos caracteres ilegibles. La función adecuada
a usar es su contraparte multibyte, `mb_substr()`.

La parte difícil es recordar utilizar las funciones `mb_*` todo el tiempo. Si se olvida incluso una sola vez, su
cadena Unicode podría quedar ilegible durante procesamientos posteriores.

No todas las funciones de cadena tienen una contraparte `mb_*`. Si no existe alguna para lo que se quiere hacer, entonces
te quedaste sin suerte.

Se Debe utilizar la función `mb_internal_encoding()` al inicio de cualquier script PHP que escriba (o al inicio de su
script de inclusión global), y la función `mb_http_output()` justo después, si su script genera salidas hacia un navegador.
Definiendo explícitamente la codificación de sus cadenas en cada script le ahorrará muchos dolores de cabeza en el futuro.

Adicionalmente, muchas funciones de PHP que operan sobre cadenas tienen un parámetro opcional que le permite especificar
la codificación de caracteres. Siempre se debe indicar explícitamente UTF-8 cuando se les da la opción. Por ejemplo,
`htmlentities()` tiene una opción para la codificación de caracteres, y siempre se debe especificar UTF-8 si se trata con este
tipo de cadenas. Tenga en cuenta que a partir de PHP 5.4.0, UTF-8 es la codificación por defecto para `htmlentities()` y
`htmlspecialchars()`.

Por último, si usted está construyendo una aplicación distribuida y no puede estar seguro de que la extensión `mbstring` estará
habilitada, considere el uso del paquete de Composer [symfony/polyfill-mbstring](https://packagist.org/packages/symfony/polyfill-mbstring).
Este usará `mbstring` si está disponible y recurrirá a funciones que no sean UTF-8 si no lo está.

[Multibyte String Extension]: https://www.php.net/es/book.mbstring
[symfony/polyfill-mbstring]: https://packagist.org/packages/symfony/polyfill-mbstring

### UTF-8 a nivel de la Base de Datos

Si su script accede a MySQL, existe la posibilidad de que sus cadenas se almacenen como cadenas no UTF-8 en la base de datos incluso
si sigue todas las precauciones anteriores.

Para asegurarse de que sus cadenas van de PHP a MySQL como UTF-8, establezca el juego de caracteres y el cotejamiento (collation) a `utf8mb4`
para su base de datos y todas sus tablas, utilice también `utf8mb4` en la cadena de conexión PDO. Vea el código de ejemplo a continuación.
Esto es de _importancia crítica_.

Tenga en cuenta de que debe usar el juego de caracteres `utf8mb4` y no `utf8` para un soporte completo UTF-8. Lea más adelante para saber por qué.

### UTF-8 a nivel del Navegador

Utilice la función `mb_http_output()` para garantizar que su script PHP genera una salida con cadenas UTF-8 hacia su navegador.

Luego, la respuesta HTTP deberá indicarle al navegador que esta página debe considerarse como UTF-8. Hoy en día, es común configurar el conjunto de caracteres en el encabezado de respuesta HTTP de esta manera:

{% highlight php %}
<?php
header('Content-Type: text/html; charset=UTF-8')
{% endhighlight %}

El enfoque histórico para hacerlo era incluir la [charset `<meta>` tag](http://htmlpurifier.org/docs/enduser-utf8.html) etiqueta `<head>` en la página.

{% highlight php %}
<?php
// Indicarle a PHP que usaremos cadenas UTF-8 hasta el final del script.
mb_internal_encoding('UTF-8');
$utf_set = ini_set('default_charset', 'utf-8');
if (!$utf_set) {
    throw new Exception('No se pudo establecer default_charset a utf-8, ¡asegúrese de que esté configurado en su sistema!');
}

// Indicarle a PHP que se imprimirá  UTF-8 al navegador

mb_http_output('UTF-8');

// Nuestra cadena de prueba UTF-8
$cadena = 'Êl síla erin lû e-govaned vîn.';

// Transforma la cadena de alguna manera con una función multibyte
// Observe cómo cortamos la cadena en un carácter que no es ASCII para fines de demostración
$cadena = mb_substr($string, 0, 15);

// Conéctese a una base de datos para almacenar la cadena transformada
// Vea el ejemplo de PDO en este documento para obtener más información
// Tenga en cuenta el `charset=utf8mb4` en el Nombre del origen de datos (DSN)
$enlace = new PDO(
    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
    'tu-nombredeusuario',
    'tu-clave',
    array(
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_PERSISTENT => false
    )
);

// Almacenamos nuestra cadena transformada como UTF-8 en nuestra base de datos
// Su base de datos y sus tablas están en el conjunto de caracteres y la intercalación utf8mb4, ¿verdad?

$handle = $enlace->prepare('insert into ElvishSentences (Id, Body, Priority) values (default, :cadena, :prioridad)');
$handle->bindParam(':cadena', $cadena, PDO::PARAM_STR);
$prioridad = 45;
$handle->bindParam(':prioridad', $prioridad, PDO::PARAM_INT); // Se le indica de forma explicita a pdo que se le dara un entero.
$handle->execute();


// Recuperamos la cadena guardada para verificar que está correctamente almacenada.
$handle = $enlace->prepare('select * from ElvishSentences where Id = :id');
$id = 7;
$handle->bindParam(':id', $id, PDO::PARAM_INT);
$handle->execute();

// Almacenamos el resultado en un objeto que nos permitirá generar HTML después
// Este objeto no tendrá efecto mayor en memoria ya que se recupera los datos por medio del método Justo a Tiempo (JIT)
$resultado = $handle->fetchAll(\PDO::FETCH_OBJ);

// Un contenedor de ejemplo que le permite escapar datos a HTML.
function escape_a_html($dirty){
    echo htmlspecialchars($dirty, ENT_QUOTES, 'UTF-8');
}

header('Content-Type: text/html; charset=UTF-8'); // Innecesario si el default_charset ya esta seteado como utf-8.
?><!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Página de prueba para UTF-8</title>
    </head>
    <body>
        <?php
        foreach($resultado as $row){
            escape_a_html($row->Body);  // Esto debería mostrar correctamente nuestra cadena UTF-8 transformada en el navegador.
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Further reading

* [PHP Manual: Operadores de Cadenas](https://php.net/manual/es/language.operators.string.php)
* [PHP Manual: Funciones de Cadenas](https://php.net/manual/es/ref.strings.php)
    * [`strpos()`](https://php.net/manual/es/function.strpos.php)
    * [`strlen()`](https://php.net/manual/es/function.strlen.php)
    * [`substr()`](https://php.net/manual/es/function.substr.php)
* [PHP Manual: Funciones de Cadenas de Caracteres Multibyte](https://php.net/manual/es/ref.mbstring.php)
    * [`mb_strpos()`](https://php.net/manual/es/function.mb-strpos.php)
    * [`mb_strlen()`](https://php.net/manual/es/function.mb-strlen.php)
    * [`mb_substr()`](https://php.net/manual/es/function.mb-substr.php)
    * [`mb_internal_encoding()`](https://php.net/manual/es/function.mb-internal-encoding.php)
    * [`mb_http_output()`](https://php.net/manual/es/function.mb-http-output.php)
    * [`htmlentities()`](https://php.net/manual/es/function.htmlentities.php)
    * [`htmlspecialchars()`](https://www.php.net/manual/es/function.htmlspecialchars.php)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](https://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](https://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [How to support full Unicode in MySQL databases](https://mathiasbynens.be/notes/mysql-utf8mb4)
* [Bringing Unicode to PHP with Portable UTF-8](https://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
* [Stack Overflow: DOMDocument loadHTML does not encode UTF-8 correctly](https://stackoverflow.com/questions/8218230/php-domdocument-loadhtml-not-encoding-utf-8-correctly)