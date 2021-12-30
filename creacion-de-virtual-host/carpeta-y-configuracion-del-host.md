# Carpeta y configuración del host



Cree el directorio para **your\_domain** de la siguiente manera:

```bash
sudo mkdir /var/www/folder_name
```

A continuación, asigne la propiedad del directorio con la variable de entorno `$USER`, que hará referencia a su usuario de sistema actual:

```bash
sudo chown -R $USER:$USER /var/www/folder_name
```

Luego, abra un nuevo archivo de configuración en el directorio `sites-available` de Apache usando el editor de línea de comandos que prefiera. En este caso, utilizaremos `nano`:

```bash
sudo nano /etc/apache2/sites-available/folder_name.conf
```

De esta manera, se creará un nuevo archivo en blanco. Pegue la siguiente configuración básica:

```
<VirtualHost *:80>
    ServerAdmin webmaster@folder_name
    ServerName folder_name
    ServerAlias www.folder_name
    DocumentRoot /var/www/folder_name
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <Directory /var/www/folder_name>
        AllowOverride All
    </Directory>
</VirtualHost>
```
