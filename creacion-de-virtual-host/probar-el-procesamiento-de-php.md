# Probar el procesamiento de PHP



Cree un archivo nuevo llamado `info.php` dentro de su carpeta root web personalizada:

```bash
nano /var/www/folder_name/info.php
```

Con esto se abrirá un archivo vacío. Añada el siguiente texto, que es el código PHP válido, dentro del archivo:

```php
<?php
phpinfo();
```

Cuando termine, guarde y cierre el archivo.

Para probar esta secuencia de comandos, diríjase a su navegador web y acceda al nombre de dominio o la dirección IP de su servidor, seguido del nombre de la secuencia de comandos, que en este caso es `info.php`:

```
http://folder_name.test/info.php
```

Si todo es correcto verá una página similar a la siguiente:

![Información de PHP de Ubuntu 20.04](https://assets.digitalocean.com/articles/lamp\_ubuntu2004/phpinfo.png)
