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
