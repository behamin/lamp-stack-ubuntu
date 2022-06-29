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

Tras añadir el PPA en nuestro equipo, debería producirse **la actualización de paquetes disponibles desde los repositorios**.

Si estás ejecutando un servidor web Apache, **se puede proceder a instalar PHP 8.0 con el módulo Apache**.&#x20;

```
sudo apt install php8.0 libapache2-mod-php8.0
```

Una vez finalizada la instalación, tendremos que **reiniciar el servidor web** [**Apache**](https://ubunlog.com/netbeans-12-1-lanzada-con-algunas-mejoras/) para habilitar el módulo.

```
sudo systemctl restart apache2
```

Llegados a este punto, ya podemos **confirmar la versión de PHP predeterminada en el servidor**:

```
php -v
```
