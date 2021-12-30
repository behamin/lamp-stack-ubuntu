# Configuración para proyecto Laravel

Una vez tiene instalado su proyecto, vamos a otorgar los permisos correspondientes:

```
sudo chown -R $USER:$USER /var/www/folder_name
sudo chmod -R 755 /var/www/folder_name
sudo chgrp -R www-data /var/www/folder_name/storage bootstrap/cache
sudo chmod -R ug+rwx /var/www/folder_name/storage bootstrap/cache
```

Creamos el **`virtual host`** y lo configuramos de la siguiente manera:

{% hint style="info" %}
Recuerda que el nombre del archivo .conf tiene que ser el mismo que el de la carpeta del proyecto
{% endhint %}

```
<VirtualHost *:80>
    ServerAdmin webmaster@folder_name
    ServerName folder_name.test
    ServerAlias www.folder_name.test
    DocumentRoot /var/www/folder_name/public
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <Directory /var/www/folder_name/public>
        AllowOverride All
    </Directory>
</VirtualHost>
```
