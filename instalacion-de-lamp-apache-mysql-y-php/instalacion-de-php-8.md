---
description: Actualización de PHP 7.4 a la versión 8.
---

# Instalación de PHP 8

PHP 7.4 es la versión predeterminada en los repositorios de Ubuntu 20.04 en el momento de escribir estas líneas. **Para poder instalar la última versión de PHP necesitaremos utilizar el repositorio de Ondrej PPA**. Este contiene múltiples versiones y extensiones de PHP.

Antes de proceder a la instalación tendremos que abrir una terminal (Ctrl+Alt+T) y **actualizar los paquetes del sistema. Además instalaremos algunas dependencias**.

```
sudo apt update; sudo apt upgrade
```

Finalizada la instalación de las dependencias, ya podemos **añadir el** [**PPA de Ondrej**](https://launchpad.net/\~ondrej/+archive/ubuntu/php). En la misma terminal, solo necesitaremos utilizar el comando:

```
sudo add-apt-repository ppa:ondrej/php
```

#### Instalar PHP 8.0 en Apache
