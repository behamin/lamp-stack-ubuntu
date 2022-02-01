# OCI8

Descarga la versión de los paquetes desde: [https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html](https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html).

En este ejemplo vamos a instalar la versión 12.2.0.1.0.

![](<../.gitbook/assets/imagen (1).png>)

Una vez descargados los archivos .zip, procedemos a crear una carpeta en la raíz de nuestro sitio llamada **oracle-client** y colocamos en esta los archivos .zip descargados.

Creamos la carpeta oracle en opt y copiamos los archivos:

```
sudo mkdir /opt/oracle
sudo cp /var/www/provare/oracle-client/instantclient-* /opt/oracle
```

Nos posicionamos en la carpeta oracle y descomprimimos los archivos:

```
cd /opt/oracle
sudo unzip instantclient-basic-linux.x64-12.1.0.2.0.zip
sudo unzip instantclient-sdk-linux.x64-12.1.0.2.0.zip
sudo unzip instantclient-sqlplus-linux.x64-12.2.0.1.0.zip
```

Eliminamos los archivos .zip:

```
sudo rm instantclient-*
```

Ahora creamos los enlaces simbólicos a los paquetes

```
sudo ln -s libclntsh.so.12.1 libclntsh.so
sudo ln -s libocci.so.12.1 libocci.so
sudo su -
echo /opt/oracle/instantclient_12_1 > /etc/ld.so.conf.d/oracle.conf
ldconfig
```

Dado que será necesario, instalamos lo siguiente:

```
sudo apt-get install php-dev php-pear build-essential libaio1
sudo pecl channel-update pecl.php.net
sudo pecl install oci8 (php 8)
sudo pecl install oci8-2.2.0  (php 7.)
```

En el último paso de la instalación te preguntará: **`if you're compiling with Oracle Instant Client [autodetect]:`** escribe lo siguiente:

```
instantclient,/opt/oracle/instantclient_12_1
```

Necesitamos decirle a PHP que cargue la extensión OCI8:

```
sudo su -
echo "extension=oci8.so" >> /etc/php/7.4/apache2/php.ini
```

Actualiza el servidor.

```
sudo shutdown -r now
```

Para terminar el proceso, habilitamos la extensión:

```
cd /etc/php/7.4/mods-available/
sudo touch oci.ini
sudo nano oci.ini
extension = oci8.so
cd /etc/php/7.4/apache2/conf.d
sudo ln -s /etc/php/7.4/mods-available/oci.ini 20-oci.ini
sudo shutdown -r now
```
