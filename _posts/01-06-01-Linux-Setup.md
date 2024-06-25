---
title:   Instalación en Linux
isChild: true
anchor:  instalacion_en_linux
---

## Instalación en Linux {#instalacion_en_linux_title}

La mayoría de las distribuciones GNU/Linux vienen con PHP disponible desde los repositorios oficiales, pero esos paquetes usualmente están un poco atrasados con respecto a la versión estable actual. Existen múltiples formas de obtener versiones más recientes de PHP en dichas distribuciones. En las distribuciones GNU/Linux basadas en Ubuntu y Debian, por ejemplo, las mejores alternativas para paquetes nativos las proporcionadas y mantenidas [Ondřej Surý][Ondrej Sury Blog], a través de su Archivo Personal de Paquetes (PPA) en Ubuntu y DPA/bikeshed en Debian. Encontrarás las instrucciones para cada uno de ellos más abajo. Dicho esto, siempre puedes usar contenedores, compilar el código fuente PHP, etc.

### Distribuciones basadas en Ubuntu

Para distribuciones Ubuntu, el [PPA de Ondřej Surý][Ondrej Sury PPA] proporciona versiones de PHP soportadas junto con muchas extensiones PECL. Para añadir este PPA a su sistema, realice los siguientes pasos en su terminal:

1. En primer lugar, añada el PPA a las fuentes de software de su sistema mediante el comando

   ```bash
   sudo add-apt-repository ppa:ondrej/php
   ```

2. Después de añadir el PPA, actualice la lista de paquetes de su sistema:

   ```bash
   sudo apt update
   ```

Esto asegurará que su sistema pueda acceder e instalar los últimos paquetes PHP disponibles en el PPA.

#### Distribuciones basadas en Debian

Para las distribuciones basadas en Debian, Ondřej Surý también proporciona un [bikeshed][bikeshed] (equivalente en Debian a un PPA). Para añadir el bikeshed a su sistema y actualizarlo, siga estos pasos:

1. Asegúrese de que tiene acceso de root. Si no es así, es posible que tenga que utilizar `sudo` para ejecutar los siguientes comandos.

2. Actualice la lista de paquetes de su sistema:

   ```bash
   sudo apt-get update
   ```

3. Instale `lsb-release`, `ca-certificates`, y `curl`:

   ```bash
   sudo apt-get -y install lsb-release ca-certificates curl
   ```

4. Descargue la clave de firma del repositorio:

   ```bash
   sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
   ```

5. Añada el repositorio a las fuentes de software de su sistema:

   ```bash
   sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
   ```

6. Por último, actualice de nuevo la lista de paquetes de su sistema:

   ```bash
   sudo apt-get update
   ```

Con estos pasos, su sistema será capaz de instalar los últimos paquetes PHP desde bikeshed.

[Ondrej Sury Blog]: https://deb.sury.org/
[Ondrej Sury PPA]: https://launchpad.net/~ondrej/+archive/ubuntu/php
[bikeshed]: https://packages.sury.org/php/
