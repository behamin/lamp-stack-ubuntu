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

Estas son las opciones que debe elegir cuando se le solicite para configurar correctamente su instalación:

* Para la selección del servidor, elija `apache2`

{% hint style="info" %}
Cuando la línea de comandos aparece, “apache2” está resaltado, pero **no** está seleccionado. Si no pulsa `SPACE` para seleccionar Apache, el instalador _no_ moverá los archivos necesarios durante la instalación. Pulse `ESPACIO,` `TAB` y luego `ENTER` para seleccionar Apache.
{% endhint %}

* Cuando se le pregunte si utiliza `dbconfig-common` para configurar la base de datos, seleccione `Yes`.
* Luego, se le solicitará elegir y confirmar una contraseña para la aplicación de MySQL para phpMyAdmin.

El proceso de instalación añade el archivo de configuración de phpMyAdmin de Apache al directorio `/etc/apache2/conhable/`, donde se lee de forma automática. Para terminar de configurar Apache y PHP a fin de que funcionen con phpMyAdmin, la única tarea que queda a continuación en esta sección del tutorial es habilitar explícitamente la extensión PHP `mbstring`. Esto se puede hacer escribiendo lo siguiente:

```bash
sudo phpenmod mbstring
```

A continuación, reinicie Apache para que sus cambios surtan efecto:

```bash
sudo systemctl restart apache2
```

phpMyAdmin ahora está instalado y configurado para funcionar con Apache. Sin embargo, pra poder iniciar sesión y comenzar a interactuar con sus bases de datos de MySQL, deberá asegurarse de que sus usuarios de MySQL tengan los privilegios necesarios para interactuar con el programa.

### Ajuste de la autenticación y los privilegios de usuario <a href="#paso-2-ajuste-de-la-autenticacion-y-los-privilegios-de-usuario" id="paso-2-ajuste-de-la-autenticacion-y-los-privilegios-de-usuario"></a>

Cuando instaló phpMyAdmin en su servidor, automáticamente creó un usuario de base de datos llamado **phpmyadmin** que realiza ciertos procesos subyacentes para el programa. En vez de registrarse como este usuario con la contraseña administrativa que estableció durante la instalación, se le recomienda iniciar sesión como **root** user de MySQL o como usuario dedicado a administrar las bases de datos a través de la interfaz de phpMyAdmin.

#### Configuración del acceso con contraseña para la cuenta root de MySQL <a href="#configuracion-del-acceso-con-contrasena-para-la-cuenta-root-de-mysql" id="configuracion-del-acceso-con-contrasena-para-la-cuenta-root-de-mysql"></a>

En los sistemas Ubuntu con MySQL 5.7 (y versiones posteriores), el usuario **root** de MySQL se configura para la autenticación usando el complemento `auth_socket` de manera predeterminada en lugar de una contraseña. En muchos casos, esto proporciona mayor seguridad y utilidad, pero también puede generar complicaciones cuando sea necesario permitir que un programa externo (como phpMyAdmin) acceda al usuario.

Si aún no lo ha hecho, deberá cambiar el método de autenticación de `auth_socket` a uno que haga uso de una contraseña, para poder acceder a phpMyAdmin como su **root** user de MySQL. Para hacer esto, abra la consola de MySQL desde su terminal:

```bash
sudo mysql
```

A continuación, compruebe con el siguiente comando el método de autenticación utilizado por una de sus cuentas de usuario de MySQL:

```bash
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

Puede ver que, en efecto, el usuario **root** se autentica utilizando el complemento de `auth_socket`. Para configurar la cuenta de **root** de modo que la autenticación se realice con una contraseña, ejecute el siguiente comando `ALTER USER`. Asegúrese de cambiar `password` por una contraseña segura que elija:

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
```

Luego, compruebe nuevamente los métodos de autenticación empleados por cada uno de sus usuarios para confirmar que **root** ya no se autentique usando el complemento `auth_socket`:

```bash
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

A continuación, cierre el shell de MySQL:

```bash
exit
```

Ahora puede acceder a la interfaz web visitando el nombre de dominio o la dirección IP pública de su servidor, con `“/phpmyadmin”`
