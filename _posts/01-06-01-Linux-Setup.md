---
title:   Instalación en Linux
isChild: true
anchor:  instalacion_en_linux
---

## Instalación en Linux {#instalacion_en_linux_title}

La mayoría de las distribuciones GNU/Linux vienen con PHP disponible desde los repositorios oficiales, pero esos paquetes usualmente están un poco atrasados con respecto a la versión estable actual. Existen múltiples formas de obtener versiones más recientes de PHP en dichas distribuciones.

### Distribuciones basadas en Ubuntu

En las distribuciones GNU/Linux basadas en Ubuntu y Debian, por ejemplo, las mejores alternativas para paquetes nativos las proporciona y mantiene [Ondřej Surý][Ondrej Sury Blog], a través de su Archivo Personal de Paquetes (PPA) en Ubuntu y DPA/bikeshed en Debian. Encontrarás las instrucciones para cada uno de ellos más abajo.

Para distribuciones Ubuntu, el [PPA de Ondřej Surý][Ondrej Sury PPA] proporciona versiones de PHP soportadas junto con muchas extensiones PECL. Para añadir este PPA a tu sistema, realiza los siguientes pasos en tu terminal:

1. En primer lugar, añade el PPA a las fuentes de software de tu sistema mediante el comando

   ```bash
   sudo add-apt-repository ppa:ondrej/php
   ```

2. Después de añadir el PPA, actualiza la lista de paquetes de tu sistema:

   ```bash
   sudo apt update
   ```

Esto asegurará que tu sistema pueda acceder e instalar los últimos paquetes PHP disponibles en el PPA.

### Distribuciones basadas en Debian

Para las distribuciones basadas en Debian, Ondřej Surý también proporciona un [bikeshed][bikeshed] (equivalente en Debian a un PPA). Para añadir el bikeshed a tu sistema y actualizarlo, sigue estos pasos:

1. Asegúrate de que tienes acceso de root. Si no es así, es posible que tengas que utilizar `sudo` para ejecutar los siguientes comandos.

2. Actualiza la lista de paquetes de tu sistema:

   ```bash
   sudo apt-get update
   ```

3. Instala `lsb-release`, `ca-certificates` y `curl`:

   ```bash
   sudo apt-get -y install lsb-release ca-certificates curl
   ```

4. Descarga la clave de firma del repositorio:

   ```bash
   sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
   ```

5. Añade el repositorio a las fuentes de software de tu sistema:

   ```bash
   sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
   ```

6. Por último, actualiza de nuevo la lista de paquetes de tu sistema:

   ```bash
   sudo apt-get update
   ```

Con estos pasos, tu sistema será capaz de instalar los últimos paquetes PHP desde bikeshed.

### Distribuciones basadas en RPM

En las distribuciones basadas en RPM (CentOS, Fedora, RHEL, etc.) puedes usar el [repositorio RPM de Remi][remi-repo] para instalar la última versión de PHP o para tener varias versiones de PHP disponibles simultáneamente.

Hay un [asistente de configuración][remi-wizard] disponible para configurar tu distribución basada en RPM.

Dicho todo esto, siempre puedes usar contenedores o compilar el código fuente de PHP desde cero.

[Ondrej Sury Blog]: https://deb.sury.org/
[Ondrej Sury PPA]: https://launchpad.net/~ondrej/+archive/ubuntu/php
[bikeshed]: https://packages.sury.org/php/
[remi-repo]: https://rpms.remirepo.net/
[remi-wizard]: https://rpms.remirepo.net/wizard/
