# Instalación de phpMyAdmin

Como non-root user, actualice el índice de paquetes de su servidor:

```bash
sudo apt update
```

Después de esto, puede instalar el paquete `phpmyadmin`. Junto con este paquete, en la [documentación oficial también se le recomienda](https://docs.phpmyadmin.net/en/latest/require.html) instalar algunas extensiones PHP en su servidor para habilitar ciertas funcionalidades y mejorar el rendimiento.

Si siguió el [tutorial de pila LAMP](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04) de los requisitos previos, varios de estos módulos se habrán instalado junto con el paquete `php`. Sin embargo, se recomienda también instalar estos paquetes:

* `php-mbstring`: módulo para administrar cadenas no-ASCII y convertir cadenas a diferentes codificaciones.
* `php-zip`: esta extensión admite la carga de archivos `.zip` a phpMyAdmin.
* `php-gd`: habilita la obtención de ayuda de [la biblioteca GD Graphics](https://en.wikipedia.org/wiki/GD\_Graphics\_Library).
* `php-json`: proporciona PHP con compatibilidad para serialización JSON.
* `php-curl`: permite que PHP interactúe con diferentes tipos de servidores utilizando diferentes protocolos.

Ejecute el siguiente comando para instalar estos paquetes en su sistema. Tenga en cuenta que el proceso de instalación requiere que tome algunas decisiones para configurar phpMyAdmin correctamente. En breve, veremos estas opciones:

```bash
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
```
