# Instalación

### Paso 1: Instalar MongoDB <a href="#paso-1-instalar-mongodb" id="paso-1-instalar-mongodb"></a>

Los repositorios oficiales del paquete de Ubuntu incluyen una versión estable de MongoDB. Sin embargo, en el momento de escribir este artículo, la versión de MongoDB disponible desde los repositorios predeterminados de Ubuntu es 3.6, mientras que la última versión estable es 4.4.

Para obtener la versión más reciente de este software, debe incluir el repositorio de paquetes dedicado de MongoDB a sus fuentes APT. A continuación, podrá instalar `mongodb-org`, un metapaquete que siempre apunta a la última versión de MongoDB.

Para comenzar, importe la clave pública GPG para la última versión estable de MongoDB. Puede encontrar el archivo de claves apropiado navegando al [servidor de claves de MongoDB](https://www.mongodb.org/static/pgp/) y buscando el archivo que incluye el número de la versión estable más reciente y termina en `.asc`. Por ejemplo, si desea instalar la versión 4.4 de MongoDB, buscará el archivo llamado **server-4.4.asc**.

Haga clic con el botón derecho sobre el archivo, y seleccione **Copiar dirección del enlace**. Luego pegue ese enlace en el siguiente comando `curl`, sustituyendo la URL resaltada:

```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
```

&#x20;

cURL es una herramienta de línea de comandos disponible en muchos sistemas operativos utilizada para transferir datos. Lee cualquier dato almacenado en la URL transmitida e imprime el contenido al resultado del sistema. En el siguiente ejemplo, cURL imprime el contenido del archivo de claves GPG y, luego, lo canaliza al siguiente comando `sudo apt-key add -`, añadiendo así la clave GPG a su lista de claves de confianza.

Además, tenga en cuenta que este comando `curl` utiliza las opciones `-fsSL` que, juntas, esencialmente indica a cURL que falle silenciosamente. Esto significa que si por cualquier motivo cURL no puede contactar con el servidor GPG, o el servidor GPG no está disponible, no añadirá accidentalmente el código del error resultante a su lista de claves de confianza.

Este comando devolverá `OK` si la clave se añadió correctamente:

```
OutputOK
```

Si desea comprobar que la clave se añadió correctamente, puede hacerlo con el siguiente comando:

```bash
apt-key list
```

&#x20;

Esto devolverá la clave de MongoDB en algún lugar de la salida:

```
Output/etc/apt/trusted.gpg
--------------------
pub   rsa4096 2019-05-28 [SC] [expires: 2024-05-26]
      2069 1EEC 3521 6C63 CAF6  6CE1 6564 08E3 90CF B1F5
uid           [ unknown] MongoDB 4.4 Release Signing Key <packaging@mongodb.com>
. . .
```

En este momento, su instalación APT aún no sabe dónde encontrar el paquete `mongodb-org` que necesita para instalar la última versión de MongoDB.

Hay dos lugares en su servidor donde APT busca fuentes en línea de paquetes para descargar e instalar: el archivo `sources.list` y el directorio `sources.list.d`. `sources.list` es un archivo que lista fuentes activas de datos APT, con una fuente por línea y las fuentes más preferidas listadas primero. El directorio `sources.list.d` le permite añadir dichas entradas `sources.list` como archivos independientes.

Ejecute el siguiente comando, que crea un archivo en el directorio `sources.list.d` llamado `mongodb-org-4.4.list`. El único contenido en este archivo es una única línea que lee `deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse`:

```bash
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
```

&#x20;

Esta única línea indica a APT todo lo que necesita saber sobre cuál es la fuente y dónde encontrarla:

* `deb`: Esto significa que la entrada de la fuente hace referencia a una arquitectura Debian regular. En otros casos, esta parte de la línea puede leer `deb-src`, lo que significa que la entrada de origen representa un código fuente de la distribución de Debian.
* `[ arch=amd64,arm64 ]`: esto especifica a qué arquitecturas deberían descargarse los datos APT. En este caso, especifica las arquitecturas `amd64` y `arm64`.
* `https://repo.mongodb.org/apt/ubuntu`: Esta es una URI que representa la ubicación en la que pueden encontrarse los datos APT. En este caso, la URI apunta a la dirección HTTPS donde se ubica el repositorio oficial de MongoDB.
* `focal/mongodb-org/4.4`: Los repositorios de Ubuntu pueden contener varias versiones diferentes. Esto especifica que solo quiere la versión `4.4` del paquete `mongodb-org` disponible para la versión `focal` de Ubuntu (“Focal Fossa”, que es el nombre en código de Ubuntu 20.04).
* `multiverse`: Esta parte apunta APT a uno de los cuatro repositorios principales de Ubuntu. En este caso, apunta al [repositorio `multiverse`](https://help.ubuntu.com/community/Repositories#Multiverse).

Tras ejecutar este comando, actualice el índice del paquete local de su servidor para que APT sepa dónde encontrar el paquete `mongodb-org`:

```bash
sudo apt update
```

&#x20;

Tras eso, puede instalar MongoDB:

```bash
sudo apt install mongodb-org
```

&#x20;

Cuando se le solicite, pulse `Y` y luego `ENTER` para confirmar que desea instalar el paquete.

Cuando el comando termine, MongoDB se instalará en su sistema. Sin embargo, aún no está listo para usarlo. A continuación, iniciará MongoDB y confirmará que funciona correctamente.

### Paso 2: Iniciar el servicio MongoDB y probar la base de datos <a href="#paso-2-iniciar-el-servicio-mongodb-y-probar-la-base-de-datos" id="paso-2-iniciar-el-servicio-mongodb-y-probar-la-base-de-datos"></a>

El proceso de instalación descrito en el paso anterior configura automáticamente MongoDB para que se ejecute como un daemon controlado por `systemd`, lo que significa que puede administrar MongoDB usando los diferentes comandos de `systemctl`. Sin embargo, este procedimiento de instalación no inicia automáticamente el servicio.

Ejecute el siguiente comando `systemctl` para iniciar el servicio MongoDB:

```bash
sudo systemctl start mongod.service
```

&#x20;

A continuación, compruebe el estado del servicio. Tenga en cuenta que este comando no incluye `.service` en la definición del archivo del servicio. `systemctl` añadirá este sufijo a cualquier argumento que pase automáticamente si no está ya presente, por lo que no es necesario incluirlo:

```bash
sudo systemctl status mongod
```

&#x20;

Este comando devolverá un resultado como el siguiente, lo que indica que el servicio está en funcionamiento:

```
Output● mongod.service - MongoDB Database Server
     Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
     Active: active (running) since Tue 2020-06-09 12:57:06 UTC; 2s ago
       Docs: https://docs.mongodb.org/manual
   Main PID: 37128 (mongod)
     Memory: 64.8M
     CGroup: /system.slice/mongod.service
             └─37128 /usr/bin/mongod --config /etc/mongod.conf
```

Tras confirmar que el servicio se está ejecutando como se espera, habilite el servicio MongoDB para que se inicie en el arranque:

```bash
sudo systemctl enable mongod
```

&#x20;

Puede verificar que la base de datos está operativa conectando con el servidor de la base de datos y ejecutando un comando de diagnóstico. El siguiente comando conectará con la base de datos y dará como resultado su versión actual, la dirección del servidor y el puerto. También devolverá el resultado del comando interno `connectionStatus` de MongoDB:

```bash
mongo --eval 'db.runCommand({ connectionStatus: 1 })'
```

&#x20;

`connectionStatus` verificará y devolverá el estado de la conexión con la base de datos. Un valor de `1` para el campo `ok` en la respuesta indica que el servidor funciona como se espera:

```
OutputMongoDB shell version v4.4.0
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("1dc7d67a-0af5-4394-b9c4-8a6db3ff7e64") }
MongoDB server version: 4.4.0
{
    "authInfo" : {
        "authenticatedUsers" : [ ],
        "authenticatedUserRoles" : [ ]
    },
    "ok" : 1
}
```

Además, tenga en cuenta que la base de datos se ejecuta en el puerto `27017` en `127.0.0.1`, la dirección local loopback que representa a **localhost**. Este es el número de puerto predeterminado de MongoDB.

A continuación, veremos cómo administrar la instancia del servidor MongoDB con `systemd`.

### Paso 3: Gestionar el servicio de MongoDB <a href="#paso-3-gestionar-el-servicio-de-mongodb" id="paso-3-gestionar-el-servicio-de-mongodb"></a>

Como se ha mencionado previamente, el proceso de instalación descrito en el Paso 1 configura MongoDB para que se ejecute como un servicio `systemd`. Esto significa que puede administrarlo usando los comandos `systemctl` estándar como haría con otros servicios del sistema Ubuntu.

Como se ha mencionado previamente, el comando `systemctl status` comprueba el estado del servicio MongoDB:

```bash
sudo systemctl status mongod
```

&#x20;

Puede detener el servicio en cualquier momento escribiendo:

```bash
sudo systemctl stop mongod
```

&#x20;

Para iniciar el servicio cuando esté detenido, ejecute:

```bash
sudo systemctl start mongod
```

&#x20;

También puede reiniciar el servidor cuando esté ejecutándose:

```bash
sudo systemctl restart mongod
```

&#x20;

En el Paso 2, ha habilitado MongoDB para que se inicie automáticamente con el servidor. Si desea desactivar el inicio automático en algún momento, escriba lo siguiente:

```bash
sudo systemctl disable mongod
```

&#x20;

A continuación, para volver a habilitarlo en el inicio, ejecute de nuevo el comando `enable`:

```bash
sudo systemctl enable mongod
```

&#x20;

Para obtener más información sobre cómo administrar los servicios `systemd`, consulte [Puntos esenciales de Systemd: Trabajar con servicios, unidades y el diario](https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal).
