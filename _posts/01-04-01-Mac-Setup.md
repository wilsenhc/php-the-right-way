---
title:   Instalación en macOS
isChild: true
anchor:  instalacion_en_macos
---

## Instalación en macOS {#instalacion_en_macos_title}

macOS viene preempaquetado con PHP pero normalmente está un poco por detrás de la última versión estable. Hay varias formas de instalar la última versión de PHP en macOS.

### Instalar PHP vía Homebrew

[Homebrew] es un gestor de paquetes para macOS que te ayuda a instalar fácilmente PHP y varias extensiones. El repositorio central de Homebrew proporciona «fórmulas» para PHP 7.4, 8.0, 8.1, 8.2 y PHP 8.3. Instala la última versión con este comando:

```
brew install php@8.3
```

Puede cambiar entre las versiones de PHP de Homebrew modificando su variable `PATH`. Alternativamente, puede usar [brew-php-switcher][brew-php-switcher] para cambiar de versión de PHP automáticamente.

También puede cambiar manualmente entre versiones de PHP desvinculando y vinculando la versión deseada:

```
brew unlink php
brew link --overwrite php@8.2
```

```
brew unlink php
brew link --overwrite php@8.3
```

### Instalar PHP vía Macports

El proyecto [MacPorts] es una iniciativa de código abierto para diseñar un sistema fácil de usar paracompilar, instalar y
actualizar software de código abierto basado en línea de comandos, X11 o Aqua en el sistema operativo macOS.

MacPorts soporta binarios pre-compilados, por lo que no necesitas recompilar cada dependencia desde los archivos tarball fuente,
esto te salva la vida si no tienes ningún paquete instalado en tu sistema.

En la actualidad, puede instalar `php54`, `php55`, `php56`, `php70`, `php71`, `php72`, `php73`, `php74`, `php80`, `php81`, `php82` o `php83` utilizando el comando `port install`, por ejemplo:

```
    sudo port install php74
    sudo port install php83
```

And you can run `select` command to switch your active PHP:

```
    sudo port select --set php php83
```

### Instalar PHP vía phpbrew

[phpbrew] es una herramienta para instalar y gestionar múltiples versiones de PHP. Esto puede ser realmente útil si dos
aplicaciones/proyectos requieren diferentes versiones de PHP, y no está utilizando máquinas virtuales.

### Instalar PHP vía el instalador de binarios Liip

Otra opción popular es [php-osx.liip.ch] que proporciona métodos de instalación de una línea para las versiones 5.3 a 7.3.
No sobrescribe los binarios PHP instalados por Apple, sino que instala todo en una ubicación separada. (/usr/local/php5).

### Compilar desde el código fuente

Otra opción que le da control sobre la versión de PHP que instala, es [compilarlo usted mismo][mac-compile].
En ese caso asegúrese de tener instalado [Xcode][xcode-gcc-substitution] o el sustituto de Apple
["Command Line Tools for XCode"] descargable desde el Centro de Desarrolladores de Apple.

### Instaladores Todo en Uno

Las soluciones listadas arriba se encargan principalmente del propio PHP, y no suministran cosas como [Apache][apache], [Nginx][nginx] o un servidor SQL.
Las soluciones "todo en uno" como [MAMP][mamp-downloads] y [XAMPP][xampp] instalarán estas otras partes del software por usted y las unirán todas,
pero la facilidad de configuración tiene como contrapartida la falta de flexibilidad.

[Homebrew]: https://brew.sh/
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://web.archive.org/web/20220505163210/https://php-osx.liip.ch/
[mac-compile]: https://www.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[apache]: https://httpd.apache.org/
[nginx]: https://www.nginx.com/
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
