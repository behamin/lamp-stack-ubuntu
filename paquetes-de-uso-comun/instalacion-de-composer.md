# Instalación de Composer

Primero, actualice la caché del administrador de paquetes ejecutando lo siguiente:

```bash
sudo apt update
```

Luego, ejecute el siguiente comando para instalar los paquetes requeridos:

```bash
sudo apt install php-cli unzip
```

Se le solicitará confirmar la instalación escribiendo `Y` y luego `ENTER`.

Una vez que haya instalado lo que se estipula en los requisitos previos, podrá proceder con la instalación de Composer.

### Descargar e instalar Composer <a href="#paso-2-descargar-e-instalar-composer" id="paso-2-descargar-e-instalar-composer"></a>

Composer ofrece una secuencia de comandos de [instalación](https://getcomposer.org/installer) escrita en PHP. La descargaremos, comprobaremos que no esté dañada y la utilizaremos para instalar Composer.

Asegúrese de posicionarse en su directorio de inicio y obtenga el instalador usando `curl`:

```bash
cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

A continuación, verificaremos que el instalador descargado coincida con el hash SHA-384 para el instalador más reciente disponible en la página [Composer Public Keys/Signatures](https://composer.github.io/pubkeys.html). A fin de facilitar el paso de verificación, puede utilizar el siguiente comando para obtener de forma programática el hash más reciente de la página de Composer y almacenarlo en una variable de shell:

```bash
HASH=`curl -sS https://composer.github.io/installer.sig`
```

Ahora, ejecute el siguiente código PHP, como se indica en la [página de descarga](https://getcomposer.org/download/) de Composer, para verificar que la secuencia de comandos de instalación se pueda ejecutar de forma segura:

```bash
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

Verá el siguiente resultado:

```bash
Installer verified
```

Si aparece el mensaje `Installer corrupt`, tendrá que volver a descargar la secuencia de comandos de instalación y verificar nuevamente si utilizó el hash correcto. Luego, repita el proceso de verificación. Cuando cuente con un instalador verificado, podrá continuar.

Para instalar `composer` de manera global, utilice el siguiente comando que lo descargará e instalará en todo el sistema como un comando llamado `composer`, en `/usr/local/bin`:

```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Verá un resultado similar a este:

```
OutputAll settings correct for using Composer
Downloading...

Composer (version 1.10.5) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer
```

Para comprobar su instalación, ejecute lo siguiente:

```bash
composer
```
