---
title:   Internacionalización y Localización
isChild: true
anchor:  i18n_l10n
---

## Internacionalización (i18n) y Localización (l10n) {#i18n_l10n_title}

_Aviso legal para los recién llegados: i18n y l10n son numerónimos, un tipo de abreviatura en la que se utilizan
números para acortar palabras. En nuestro caso, la internacionalización se convierte en i18n y la localización, en l10n._

En primer lugar, necesitamos definir esos dos conceptos similares y otras cosas relacionadas:

- La **internacionalización** es cuando organizas tu código de tal forma que pueda adaptarse a diferentes idiomas o
regiones sin refactorizaciones. Esta acción se realiza normalmente una vez, preferiblemente al principio del proyecto,
o de lo contrario probablemente necesitarás realizar cambios enormes en el código fuente.

- La **localización** ocurre cuando adaptas la interfaz (principalmente) traduciendo contenidos, en función del trabajo
de i18n realizado anteriormente. Por lo general, se realiza cada vez que un nuevo idioma o región necesita soporte y se
actualiza cuando se agregan nuevas partes de la interfaz, ya que deben estar disponibles en todos los idiomas compatibles.

- La **pluralización** define las reglas necesarias entre distintos idiomas para interoperar cadenas que contienen números y
contadores. Por ejemplo, en inglés, cuando solo tienes un elemento, es singular y todo lo que sea diferente se llama plural;
el plural en este idioma se indica agregando una S después de algunas palabras y, a veces, cambia partes de la palabra.
En otros idiomas, como el ruso o el serbio, hay dos formas plurales además del singular; incluso es posible encontrar
idiomas con un total de cuatro, cinco o seis formas, como el esloveno, el irlandés o el árabe.

## Formas comunes de implementación
La forma más fácil de internacionalizar aplicaciones PHP es mediante el uso de archivos de array y utilizar dichas cadenas
de texto en plantillas, como por ejemplo `<h1><?=$TRANS['title_about_page']?></h1>`. Sin embargo, esta forma no se
recomienda para proyectos serios, ya que plantea algunos problemas de mantenimiento en el camino; algunos pueden aparecer
al principio, como la pluralización. Por lo tanto, no intente esto si su proyecto contiene más de un par de páginas.

La forma más clásica y que a menudo se toma como referencia para i18n y l10n es una [herramienta Unix llamada `gettext`][gettext]
. Data de 1995 y sigue siendo una implementación completa para traducir software. Es bastante fácil de poner en funcionamiento,
mientras que todavía cuenta con potentes herramientas de soporte. Hablaremos aquí sobre Gettext. Además, para ayudarte a no
complicarte en la línea de comandos, presentaremos una excelente aplicación GUI(interfaz gráfica de usuario) que se puede
usar para actualizar fácilmente tu fuente l10n.

### Otras herramientas

Hay librerías de uso común que soportan Gettext y otras implementaciones de i18n. Algunas de ellas pueden parecer más fáciles
de instalar, tener características adicionales, o formatos de archivo i18n. En este documento, nos centramos en las herramientas
proporcionadas con el núcleo de PHP, pero enumeramos otras para complementar:

- [aura/intl][aura-intl]: proporciona herramientas de internacionalización (I18N), específicamente traducción de mensajes por
configuración regional orientada a paquetes. Utiliza formatos de matriz para los mensajes. No proporciona un extractor de
mensajes, pero sí proporciona un formato de mensajes avanzado a través de la extensión `intl` (incluidos los mensajes en plural).
- [php-gettext/Gettext][php-gettext]: soporte para Gettext con una interfaz orientada a objetos; incluye funciones de ayuda
mejoradas, extractores poderosos para varios formatos de archivo (algunos de ellos no soportados de forma nativa por el comando
`gettext`) y también puede exportar a otros formatos además de los archivos `.mo/.po`. Puede ser útil si necesita integrar
sus archivos de traducción en otras partes del sistema, como una interfaz de JavaScript.
- [symfony/translation][symfony]: admite muchos formatos diferentes, pero recomienda utilizar XLIFF detallados. No incluye funciones
auxiliares ni un extractor integrado, pero admite texto provisionales(placeholders) mediante `strtr()` internamente.
- [laminas/laminas-i18n][laminas]: admite archivos de matriz e INI, o formatos Gettext. Implementa una capa de almacenamiento en caché
para evitar que tenga que leer el sistema de archivos cada vez. También incluye ayudantes de visualización, filtros y validadores de
entrada que tienen en cuenta la configuración regional. Sin embargo, no tiene un extractor de mensajes.

Otros marcos de trabajo(frameworks) también incluyen modulos i18n, pero estos no estan disponibles fuera de su codigo.

- [Laravel] soporta archivos con matrices básicas, no tiene extractor automático pero incluye un helper `@lang` para archivos de plantilla.
- [Yii] soporta matrices, Gettext, y traducciones por medio de bases de datos, además incluye un extractor de mensajes. es soportado por
la extensión [`Intl`][intl], disponible desde la versión php 5.3, y basada en el [ICU project]; esto permite a Yii correr poderosos
reemplazos, como la representación en palabras de números, fechas formateadas, hora, intervalo, monedas, y ordinales.

Si decides escoger una de las librerías que no proveen extractor, podrías querer utilizar el formato gettext, así puedes
utilizar las utilidades de **gettext** (incluyendo Poedit) como han sido descritas en el resto del capítulo.

## Gettext

### Instalacion
Podrias necesitar instalar Gettext y el resto de librerías php relacionadas por medio de tu manejador de paquetes,
como `apt-get` o `yum`. luego de instalado, debes activarlo agregando ya sea `extension=gettext.so` si estas en Linux/Unix o
`extension=php_gettext.dll` si estas en Windows, a tu archivo `php.ini`.

También se estará utilizando [Poedit] para crear archivos de traducción. Es probable que lo encuentres en el manejador de
paquetes de tu sistema; Está disponible para Unix, macOS, y Windows, además puede ser descargado [gratis en su web][poedit_download].

### Estructura

#### TIpos de archivos
Existen 3 tipos de archivos que se suelen utilizar cuando se trabaja con gettex. los principales son los archivos
PO (objeto portable) y MO (objeto máquina), el primero siendo una lista de "objetos traducidos" leible y el segundo,
los binarios correspondientes que serán interpretados por gettext mientras se realiza la localización. Además también
existe un archivo POT (plantilla), el que simplemente contiene todas las llaves existentes de tu código fuente, y puede
ser utilizado como una guía para generar y actualizar todos los archivos PO. Estos archivos plantilla no son obligatorios:
depende de la herramienta que estés utilizando para realizar l10n, podría ser suficiente con solo los archivos PO/MO.
Siempre tendrás una pareja de archivos PO/MO por cada lenguaje y región, pero solo un archivo un archivo POT por dominio.

### Dominios
Existen algunos casos, en grandes proyectos, donde podría ser necesario separar la traducción cuando una misma palabra
puede tener un significado diferente dependiendo del contexto. En esos casos, puedes separarla en diferentes _dominios_.
Ellos son, básicamente, grupos nombrados de archivos POT/PO/MO, donde los nombres de los archivos son el _dominio de traducción_.
Proyecto pequeños y medianos suelen, por simplicidad, utilizan un solo dominio; el nombre es arbitrario, pero utilizaremos
"principal" en los códigos de ejemplo. In los proyectos [Symfony], por ejemplo, los dominios son utilizados para separar
la traducción para los mensajes de validación.

#### Codigo local
Un local es un código sencillo que identifica una versión de un lenguaje. Está definido siguiendo las especificaciones de
los estándar [ISO 639-1][639-1] y [ISO 3166-1 alpha-2][3166-1]: dos letras en minúsculas para el lenguaje, opcionalmente
puede estar seguido por un guión bajo y dos letras mayúsculas identificando el país o el código regional. para
[lenguajes extraños][rare], tres letras son utilizados.

Para algunos parlantes, el país puede parecer redundante. De hecho, algunos lenguajes tienen diferentes dialectos
en diferentes países, tal es el caso de Aleman Australiano (`de_AT`) o el Portugués de Brasil (`pt_BR`). la segunda
parte es utilizado para distinguir entre estos dos dialectos - cuando no está presente, se coma como una versión "genérica"
o "híbrida" del lenguaje.

### Estructura del directorio
Para utilizar Gettext, primero necesitamos seguir una estructura específica de archivos. Primero, se tiene que seleccionar
una carpeta raíz arbitraria para los archivos l10n en tu código fuente. Dentro de esta, se tendrá una carpeta por cada local,
y una carpeta `LC_MESSAGES` que contendrá todos los pares PO/MO. Ejemplo:

{% highlight console %}
<project root>
 ├─ src/
 ├─ templates/
 └─ locales/
    ├─ forum.pot
    ├─ site.pot
    ├─ de/
    │  └─ LC_MESSAGES/
    │     ├─ forum.mo
    │     ├─ forum.po
    │     ├─ site.mo
    │     └─ site.po
    ├─ es_ES/
    │  └─ LC_MESSAGES/
    │     └─ ...
    ├─ fr/
    │  └─ ...
    ├─ pt_BR/
    │  └─ ...
    └─ pt_PT/
       └─ ...
{% endhighlight %}

### Forma Plural
Como se dijo en la introducción, diferentes lenguajes pueden tener diferentes formas plurales. Sin embargo, gettext te
ahorra estos problemas. Cuando se crea un nuevo archivo `.po`, tendrás que declarar las [reglas plurales][plural] para
ese lenguaje, y las piezas traducidas que son sensitivas al plural tendrán una forma para cada una de estas reglas. Cuando
se llame a Gettext en el código, necesitará especificar la cantidad relacionada a la oración, y el se encargara de
usar la forma correcta - incluso utilizar sustitución de cadena de ser necesario.

Las reglas de plural incluyen la cantidad de plurales disponibles y una prueba booleana con `n` que definiría en qué
regla se encuentra el número dado (comenzando el conteo con 0). Por ejemplo:

- Japonés: `nplurals=1; plural=0` - Solo una reglas.
- Inglés: `nplurals=2; plural=(n != 1);` - 2 reglas, la primera si n es igual a 1, la segunda si es diferente a 1.
- Portugués de Brasil: `nplurals=2; plural=(n > 1);` - 2 Reglas, segunda si n es mayor a uno, la primera si no lo es.

Ahora que comprendes las bases de cómo funcionan las reglas para el plural - y en caso de que no, por favor lee una
explicacion mas a fondo [LingoHub tutorial][lingohub_plurals] -, podrias querer copias las que necesitas es una
[lista][plural] en lugar de escribirlas a mano.

Cuando invocas a Gettext para realizar una localización en **oraciones** con contadores, necesitarás proveer también
el número relacionado. Gettext determinará las reglas que se deben aplicar y usará la versión de localización correcta.
Necesitarás incluir en el archivo `.po` una sentencia diferente por cada regla plural definida.

### Ejemplo de implementación
Luego de tanto teoría, es momento de ir a la práctica. Aquí un fragmento de un archivo `.po` - no le prestes atención
a su formato, si no a su contenido general; Luego aprenderás como editarlo fácilmente.

{% highlight po %}
msgid ""
msgstr ""
"Language: pt_BR\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"

msgid "Estamos traduciendo algunas cadenas"
msgstr "Nós estamos traduzindo algumas strings agora"

msgid "Hola %1$s! tu última visita fue el %2$s"
msgstr "Olá %1$s! Sua última visita foi em %2$s"

msgid "Solo un mensaje sin leer"
msgid_plural "%d mensajes sin leer"
msgstr[0] "Só uma mensagem não lida"
msgstr[1] "%d mensagens não lidas"
{% endhighlight %}

La primera sección funciona como una cabecera, teniendo los `msgid` and `msgstr` vacios(mensaje id, mensaje string). Esta describe el **encoding* del
archivo, la forma plural y otras cosas son menos relevantes.
La segunda sección traduce una cadena sencilla desde el español al Portuges de Brasil, y la tercera hace lo mismo, pero
utilizando el reemplazo de cadena de [`sprintf`][sprintf] así la traducción puede contener el nombre y la fecha de visita.
La últimas sección es un muestra de la forma de pluralización, mostrando tanto la forma singular y plural como `msgid` en
español, y su traducción correspondiente como `msgstr` 0 y 1 (siguiendo los números dado en las reglas de forma plural). aquí,
el reemplazo de cadena es utilizado también para que el número puede ser visto directamente en la sentencia. con el uso de `%d`.
La forma plural siempre tiene dos `msgid` (singular y plural), por lo que es aconsejado no utilizar un lenguaje complicado
como base del recurso de traducción.

### Discusion en l10n llaves
Como podrás haber notado, estamos utilizando como recurso de id la sentencia en español. ese `msgid` será el mismo
utilizado en todos tus archivos `.po`, por lo que los otros lenguajes tendrán el mismo formato y el mismo campo `msgid`
pero líneas `msgstr` traducidas.
Hablando de llaves de traduccion, existen 2 vertientes principales:

1. _`msgid` como una sentencia real_.
   La ventaja principal sería:
   - Si hay partes del programa sin traducir en algún lenguaje en específico, la llave mostrada mantendrá algún un poco
   poco del significado. Por ejemplo: si eres capaz de traducir de Español a Ingles sin ningun problema, pero necesitas algo
   de ayuda para traducir al francés, podrias publicar primero la página faltando algunas traducciones de sentencias en
   Francés, y parte de la interfaz en local Francés será mostrado en español en su lugar;
   - Es mucho más fácil para el traductor entender el contexto y realizar una traducción apropiada basado en el `msgid`.
   - Te da un l10 "gratis" para un lenguaje - el principal;
   - La única desventaja: si necesitas cambiar el texto actual, tendrías que reemplace el mismo `msgid` en todos los
   archivos de lenguaje.

2. _`msgid` as a unique, structured key_.
Esta describiría el rol de la sentencia en la aplicación de una forma estructurada, incluyendo la plantilla o parte
donde la cadena está ubicada actualmente en lugar de su contenido.
   - Es una gran manera de tener el código organizado, separando el contenido del texto de la lógica de la plantilla.
   - Sin embargo, esto podría traerle problemas al traductor que perdería el contexto. Un archivo de lenguaje principal
   sería necesario como una base para las otras traducciones. Ejemplo: el desarrollador tendrá idealmente un archivo
   `es.po`, que el traductor tendría que leer para entender que debería escribir, por ejemplo, en `fr.po`.
   - Traducciones faltantes mostrarían llaves sin un claro significado (`menu_principal.bienvenido` en lugar de
   `Hola, sea bienvenido`). Lo positivo es que forzará la traducción a estar completa antes de publicar la app - sin
   embargo, tan mal como podrían ser problemas de traducción en la interfaz. Algunas librerías incluyen una opción para
   especificar un lenguaje de respaldo, obteniendo así un comportamiento parecido a la estrategia anterior.

El [manual Gettext][manual] favorece la primera estrategia debido a que, en general, es más fácil para los traductores
y usuarios en caso de problema. Por lo que esa es la forma en la que trabajaremos aquí. Sin embargo, la
[Documentación de Symfony][symfony-keys] favorece la traducción basada en **palabras claves**, para permitir cambios
independientes de todas las traducciones sin afectar a las plantillas.

### Uso Usual
En una aplicación típica, utilizar algunas funciones Gettext mientras escribes texto estático en tus páginas. Estas
sentencias aparecen en los archivos `.po`, se traducirían, compilaron en archivos `.mo` y entonces, serían utilizados
por Gettext cuando se renderiza la interfaz actual. Con lo anterior, armemos todo lo que se ha discutido hasta el momento en
un ejemplo paso a paso:

#### 1. Un simple archivo plantilla, incluyendo diferentes llamadas gettext.
{% highlight php %}
<?php include 'i18n_setup.php' ?>
<div id="cabecera">
    <h1><?=sprintf(gettext('Bienvenido, %s!'), $nombre)?></h1>
    <!-- código indentado de esta forma solo para mejorar la lectura -->
    <?php if ($sinLeer): ?>
        <h2><?=sprintf(
            ngettext('Un mensaje sin leer',
                     '%d mensajes sin leer',
                     $sinLeer),
            $sinLeer)?>
        </h2>
    <?php endif ?>
</div>

<h1><?=gettext(''Introducción'')?></h1>
<p><?=gettext('Ahora estamos traduciendos algunos textos')?></p>
{% endhighlight %}

- [`gettext()`][func] Simplemente traduce un `msgid` a su `msgstr` correspondiente para un lenguaje especificado. También
existe una funcion corta `_()` que trabaja de la misma manera.
- [`ngettext()`][n_func] hace lo mismo pero con reglas de plural;
- También tenemos a [`dgettext()`][d_func] y [`dngettext()`][dn_func], que permite sobreescribir el dominio de la próxima
llamada. Más sobre configuración de dominios en el próximo ejemplo.that allow you to override the domain for a single


#### 2. Un archivo demostrativo (`i18n_setup.php` como se utilizó en el ejemplo anterior), seleccionando el local correcto y

Configurando Gettext.
{% highlight php %}
<?php
/**
 * Verifica si el $local especificado es soportado en el proyecto
 * @param string $local
 * @return bool
 */
function valido($local) {
   return in_array($local, ['en_US', 'en', 'pt_BR', 'pt', 'es_ES', 'es']);
}

//especificando el local por defecto, para propósitos informativos.
$lang = 'en_US';

if (isset($_GET['lang']) && valid($_GET['lang'])) {
    // El local puede ser cambiado por medio del **query-string**
    $lang = $_GET['lang'];    //deberías sanitizar esto!..
    setcookie('lang', $lang); //Se almacena en una cookie para que así pueda ser reutilizado.
} elseif (isset($_COOKIE['lang']) && valid($_COOKIE['lang'])) {
    // Si esta presenta la cookie, se utiliza su valor.
    $lang = $_COOKIE['lang']; //deberías sanitizar esto!.
} elseif (isset($_SERVER['HTTP_ACCEPT_LANGUAGE'])) {
    // defecto: Determinar cuál es el lenguaje que el navegador dice que el usuario acepta.
    $langs = explode(',', $_SERVER['HTTP_ACCEPT_LANGUAGE']);
    array_walk($langs, function (&$lang) { $lang = strtr(strtok($lang, ';'), ['-' => '_']); });
    foreach ($langs as $browser_lang) {
        if (valid($browser_lang)) {
            $lang = $browser_lang;
            break;
        }
    }
}

// Aquí definiremos el sistema local global en base al lenguaje obtenido.
putenv("LANG=$lang");

// Esto podría ser útil para funciones de fecha (LC_TIME) o formateo de dinero (LC_MONETARY).
setlocale(LC_ALL, $lang);

// Esto hará que Gettext busque en ../locales/<lang>/LC_MESSAGES/main.mo
bindtextdomain('main', '../locales');

// Indica el codificado que se debe utilizar para leer el archivo.
bind_textdomain_codeset('main', 'UTF-8');

// Si tu aplicación tiene dominios adicionales, como mencioné anteriormente, deberías enlazarlos todos aquí también.
bindtextdomain('forum', '../locales');
bind_textdomain_codeset('forum', 'UTF-8');

// Aquí indicamos el dominio por defecto que las llamadas gettext() deberían utilizar.
textdomain('main');

// Esto buscará la cadena en forum.mo en lugar de main.mo.
// echo dgettext('forum', 'Welcome back!');
?>
{% endhighlight %}

#### 3. Preparando las traduccion para la primer ejecucion.
Una de las grandes ventajas de Gettext tiene sobre paquetes custom i18n de marcos de trabajoes su extensivo y poderoso
formato de archivo. "Rayos, esto es muy complicado para entender y editar a mano, una matriz sería mucho más sencillo!"
No te confundas, aplicaciones como [Poedit] están aquí para ayudarte - _mucho_. Puedes obtener el program desde
[su sitio oficial][poedit_download], es gratis y está disponible en todas las plataformas. Es una herramienta muy
sencilla de utilizar, y además una muy poderosa - utilizando todas las características que Gettext tiene disponible.
Esta guía está basada en PoEdit 1.8.

En la primera ejecución, debes seleccionar “File > New...” desde el menú. Se te preguntará directamente por el idioma:
aquí puedes seleccionar/filtrar los lenguajes a los que quieres traducir, o utiliza el formato que mencionamos anteriormente,
como son `en_US` o `pt_BR`.

Luego, guarda el archivo - utilizando la estructura de directorios ya mencionados. Después deberías darle click a
“Extract from sources”, y aquí configuraras varias opciones para las tareas de extracción y traducción. Serás capaz de
encontrar esto luego en el menú “Catalog > Properties”:

-Source paths: Aquí debes incluir todos las carpetas del proyecto donde `gettext()` (y hermanos) son llamados -
esta será usualmente tu carpeta de plantillas/vistas. Este es la única configuración obligatoria.

- Translation properties(propiedades de traducción):
	- Project name and version, Team and Team’s email address: información importante que va en la cabecera de tu
	  archivo .po;
	- Plural forms: Aqui van las reglas que mencionamos anteriormente - aquí existe un enlace con ejemplos
	  Puedes dejarlo con las opciones por defecto en la mayoría de los casos, ya que PoEdit incluye un base de datos
	   muy util que contiene reglas de plural para muchos lenguajes.
	- Charsets: UTF-8, preferiblemente;
	- Source code charset: Especifica el codificado utilizado en tu código - lo más probable es que sea también
	  UTF-8.
	- Source keyword: El código que corre detrás conocido como `gettext()` y llamadas a funciones similares en diferentes
   	lenguajes de programación, además podrías crear tus propias funciones de traducción. Aquí sería donde agregarías
   	todos esos métodos. De esto se discutirá luego en la sección de "tips".

Luego de especificar todos esos puntos ejecuta un escaneo a tu archivos fuente y encontrará todas las llamadas a
localización. Luego de cada escaneo PoEdit mostrará un resumen de lo que fue encontrado y lo que fue removido en
dichos archivos. Las nuevas entradas se cargaran vacías en las tablas de traducción, y comenzaras a escribir en las
versiones localizadas de esas cadenas de texto. Guarda y un archivo `.mo` será (re)compilado en la misma carpeta
y listo!: tu proyecto está internacionalizado.

#### 4. Cadenas de texto para traducción
Cómo podrías haber notado, existen dos tipos principales de cadenas para localización, las sencillas y aquellas con
formas plural. La primera solo tiene dos cajas sencillas: source(fuente) y localized string (cadena localizada). La cadena
fuente no puede ser modifica debido a que Gettext/Poedit no incluye la capacidad de alterar tus archivos fuente - Tu
deberás cambiar el origen directamente y volver a escanear los archivos. Consejo: puedes darle click derecho a una
línea de traducción y este te dará una pista del archivo origen y la línea donde esa cadena de texto está siendo
utilizada.
Por otro lado, las cadenas de forma plural tienen dos cajas para mostrar las dos cadenas fuente, y pestañas para
que puedas configurar las diferentes formas finales.

Cada vez que cambies tus fuentes y necesites actualizar las traducciones, solo presiona Refresh y Poedit volverá a
escanear el Código, removiendo entradas inexistentes, fusionando las que han cambiado con las que se han agregado.
Incluso podría intentar adivinar algunas de las traducciones, basado en otras que has realizado. Esas conjeturas y las
entradas cambiadas recibirán una marca "Fuzzy", indicando que requiere verificación, mostrándose dorados en el listado.
También es útil si tienes un equipo de traducción y alguien intenta escribir algo sobre lo que no esta seguro: solo necesita
marcar "Fuzy", y alguien más lo verifica luego.

Finalmente, es aconsejado dejar "View > Untranslated entries first" marcado, ya que esto ayudará _mucho_ a no
olvidar ninguna entrada. Desde ese menú, también puedes abrir otras partes de la UI que te permiten dejar
información contextual para los traductores de ser necesarios.

### Tips & Tricks

#### Possible caching issues

Si está ejecutando PHP como un módulo en Apache (`mod_php`), puedes tener problemas con el almacenamiento en
caché del archivo `.mo`. Esto sucede la primera vez que se lee y, luego, para actualizarlo, es posible que deba reiniciar
el servidor. En Nginx y PHP5, generalmente solo se necesitan un par de actualizaciones de página para actualizar el
caché de traducción y, en PHP7, rara vez es necesario.

#### Additional helper functions

Como prefieren muchas personas, es más fácil usar `_()` en lugar de `gettext()`. Muchas bibliotecas i18n personalizadas
de frameworks también usan algo similar a `t()` para hacer que el código traducido sea más corto. Sin embargo, esa
es la única función que tiene un atajo. Es posible que desee agregar en su proyecto algunas otras, como `__()` o `_n()`
para `ngettext()`, o tal vez un `_r()` sofisticado que uniría las llamadas `gettext()` y `sprintf()`. Otras bibliotecas, como
[Gettext de php-gettext][php-gettext] también proporcionan funciones auxiliares como estas.

En esos casos, necesitarás indicarle a la utilidad Gettext cómo extraer las cadenas de esas nuevas funciones. No
temas; es muy fácil. Es solo un campo en el archivo `.po`, o una pantalla de Configuración en Poedit. En el editor,
esa opción está dentro de "Catalog > Properties > Source keywords". Recuerda: Gettext ya conoce las
funciones predeterminadas para muchos idiomas, así que no temas si esa lista parece vacía. Debes incluir allí las
especificaciones de esas nuevas funciones, siguiendo [un formato específico][func_format]:

- si creas algo como `t()` que simplemente devuelve la traducción de una cadena, puedes especificarlo como
`t`. Gettext sabrá que el único argumento de la función es la cadena que se va a traducir;
- Si la función tiene más de un argumento, puedes especificar en cuál de ellos está la primera cadena - y si
es necesario, también la forma plural. Por ejemplo, si llamamos a nuestra función de esta manera: `__('one user', '%d users', $number)`,
la especificación sería `__:1,2`, lo que significa que la primera forma es el primer argumento y la segunda
forma es el segundo argumento. Si tu número viene como el primer argumento, la especificación sería
`__:2,3`, lo que indica que la primera forma es el segundo argumento, y así sucesivamente.

Después de incluir esas nuevas reglas en el archivo `.po`, un nuevo escaneo traerá sus nuevas cadenas con la misma
facilidad que antes.

### References

* [Wikipedia: i18n and l10n](https://en.wikipedia.org/wiki/Internationalization_and_localization)
* [Wikipedia: Gettext](https://en.wikipedia.org/wiki/Gettext)
* [LingoHub: PHP internationalization with gettext tutorial][lingohub]
* [PHP Manual: Gettext](https://www.php.net/manual/book.gettext.php)
* [Gettext Manual][manual]

[Poedit]: https://poedit.net
[poedit_download]: https://poedit.net/download
[lingohub]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/
[lingohub_plurals]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/#Plurals
[plural]: https://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html
[gettext]: https://en.wikipedia.org/wiki/Gettext
[manual]: https://www.gnu.org/software/gettext/manual/gettext.html
[639-1]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[3166-1]: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[rare]: https://www.gnu.org/software/gettext/manual/gettext.html#Rare-Language-Codes
[func_format]: https://www.gnu.org/software/gettext/manual/gettext.html#Language-specific-options
[aura-intl]: https://github.com/auraphp/Aura.Intl
[php-gettext]: https://github.com/php-gettext/Gettext
[symfony]: https://symfony.com/components/Translation
[laminas]: https://docs.laminas.dev/laminas-i18n/
[laravel]: https://laravel.com/docs/master/localization
[yii]: https://www.yiiframework.com/doc/guide/2.0/en/tutorial-i18n
[intl]: https://www.php.net/manual/intro.intl.php
[ICU project]: https://icu.unicode.org/
[symfony-keys]: https://symfony.com/doc/current/translation.html#using-real-or-keyword-messages

[sprintf]: https://www.php.net/manual/function.sprintf.php
[func]: https://www.php.net/manual/function.gettext.php
[n_func]: https://www.php.net/manual/function.ngettext.php
[d_func]: https://www.php.net/manual/function.dgettext.php
[dn_func]: https://www.php.net/manual/function.dngettext.php
