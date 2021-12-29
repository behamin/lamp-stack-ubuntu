# Instalación de PHP



PHP es el componente de nuestra configuración que procesará el código para mostrar contenido dinámico al usuario final. Además del paquete `php`, necesitará `php-mysql`, un módulo PHP que permite que este se comunique con bases de datos basadas en MySQL. También necesitará `libapache2-mod-php` para habilitar Apache para gestionar archivos PHP. Los paquetes PHP básicos se instalarán automáticamente como dependencias.

Para instalar estos paquetes, ejecute lo siguiente:

```bash
sudo apt install php libapache2-mod-php php-mysql
```

&#x20;

Una vez que la instalación se complete, podrá ejecutar el siguiente comando para confirmar su versión de PHP:

```bash
php -v
```
