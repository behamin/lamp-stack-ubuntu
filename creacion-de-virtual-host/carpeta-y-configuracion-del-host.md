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
    ServerName folder_name.test
    ServerAlias www.folder_name.test
    DocumentRoot /var/www/folder_name
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <Directory /var/www/folder_name>
        AllowOverride All
    </Directory>
</VirtualHost>
```

Ahora, puede usar `a2ensite` para habilitar el nuevo host virtual:

```bash
sudo a2ensite folder_name.conf
```

Para asegurarse de que su archivo de configuración no contenga errores de sintaxis, ejecute lo siguiente:

```bash
sudo apache2ctl configtest
```

Vuelva a cargar Apache para que estos cambios surtan efecto:

```bash
sudo systemctl reload apache2 o sudo service apache2 restart
```

Por último configuramos nuestro archivo host virtual local :&#x20;

```
sudo nano /etc/hosts
```

Añadimos nuestro host:

```
127.0.1.1     folder_name.test
```

{% hint style="info" %}
Si su entorno de trabajo es Windows necesitará configurar el host en el archivo de host de windows ubicado en la siguiente dirección: C:\WINDOWS\system32\drivers\etc\host
{% endhint %}

Cree un archivo `index.html` en esa ubicación para poder probar que el host virtual funcione según lo previsto:

```bash
nano /var/www/folder_name/index.html
```

Incluya el siguiente contenido en este archivo:

```bash
<h1>It works!</h1>

<p>This is the landing page of <strong>folder_name</strong>.</p>
```

Listo! Si todo ha ido bien podrá acceder a su nuevo virtual host:

```
http://folder_name.test:host_port(Puerto anfitrión)
```
