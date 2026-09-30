---
title:   Instalación en Linux
isChild: true
anchor:  instalacion_en_linux
---

## Instalación en Linux {#instalacion_en_linux_title}

Most GNU/Linux distributions come with PHP available from the official repositories, but those packages usually are a little behind the current stable version. There are multiple ways to get newer PHP versions on such distributions.

### Distribuciones basadas en Ubuntu

On Ubuntu and Debian-based GNU/Linux distributions, for instance, the best alternatives for native packages are provided and maintained by [Ondřej Surý][Ondrej Sury Blog], through his Personal Package Archive (PPA) on Ubuntu and DPA/bikeshed on Debian. Find instructions for each of these below.

For Ubuntu distributions, the [PPA by Ondřej Surý][Ondrej Sury PPA] provides supported PHP versions along with many PECL extensions. To add this PPA to your system, perform the following steps in your terminal:

1. En primer lugar, añada el PPA a las fuentes de software de su sistema mediante el comando

   ```bash
   sudo add-apt-repository ppa:ondrej/php
   ```

2. Después de añadir el PPA, actualice la lista de paquetes de su sistema:

   ```bash
   sudo apt update
   ```

Esto asegurará que su sistema pueda acceder e instalar los últimos paquetes PHP disponibles en el PPA.

### Debian-based distributions

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

### RPM-based distributions

On RPM-based distributions (CentOS, Fedora, RHEL, etc.) you can use the [Remi's RPM repository][remi-repo] to install the latest PHP version or to have multiple PHP versions simultaneously available.

There is a [configuration wizard][remi-wizard] available to configure your RPM-based distribution.

All that said, you can always use containers or compile the PHP source code from scratch.

[Ondrej Sury Blog]: https://deb.sury.org/
[Ondrej Sury PPA]: https://launchpad.net/~ondrej/+archive/ubuntu/php
[bikeshed]: https://packages.sury.org/php/
[remi-repo]: https://rpms.remirepo.net/
[remi-wizard]: https://rpms.remirepo.net/wizard/
