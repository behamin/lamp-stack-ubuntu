# Configuración SLL

Creamos la certificación

```
sudo openssl genrsa -out ca.key 2048
sudo openssl req -nodes -new -key ca.key -out ca.csr
```

```
Country Name (2 letter code) [AU]:ES
State or Province Name (full name) [Some-State]:PROVINCIA
Locality Name (eg, city) []:CIUDAD
Organization Name (eg, company) [Internet Widgits Pty Ltd]:NOMBRE EMPRESA               
Organizational Unit Name (eg, section) []:DEPARTAMENTO
Common Name (e.g. server FQDN or YOUR name) []:nombre_carpeta_proyecto                              
Email Address []:EMAIL

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:OPCIONAL "ENTER"
An optional company name []:OPCIONAL "ENTER"

```

Generamos el certificado (ca.crt) del tipo X509 válido para 365.

```
sudo openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt
```

Copiamos los certificados generados en el directorio “/etc/apache2/ssl”

```
sudo cp ca.crt ca.key ca.csr /etc/apache2/ssl/
```

Para terminar, editamos el **`virtual host` **&#x20;

```
sudo nano /etc/apache2/sites-available/nombre_del_archivo.conf
```

Copia y pega esta estructura, edítala con los datos y garda los cambios.

```
<VirtualHost *:443>
    ServerAdmin admin@argon.test
    ServerName argon.test
    ServerAlias www.argon.test
    DocumentRoot /var/www/argon.test/public
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/ca.crt
    SSLCertificateKeyFile /etc/apache2/ssl/ca.key
    <Directory /var/www/argon.test/public>
        AllowOverride All
    </Directory>
</VirtualHost>
```

Habilitamos y reiniciamos apache

```
sudo a2enmod ssl
sudo a2enmod rewrite
sudo service apache2 restart
```

Ahora deberías de poder acceder con https://
