# Instalación de MySQL

Ahora que dispone de un servidor web funcional, deberá instalar un sistema de base de datos para poder almacenar y gestionar los datos de su sitio. MySQL es un sistema de administración de bases de datos popular que se utiliza en entornos PHP.

Una vez más, utilice `apt` para adquirir e instalar este software:

```bash
sudo apt install mysql-server
```

&#x20;

Cuando se le solicite, confirme la instalación al escribir `Y` y, luego, `ENTER`.

Cuando la instalación se complete, se recomienda ejecutar una secuencia de comandos de seguridad que viene preinstalada en MySQL Con esta secuencia de comandos se eliminarán algunos ajustes predeterminados poco seguros y se bloqueará el acceso a su sistema de base de datos. Inicie la secuencia de comandos interactiva ejecutando lo siguiente:

```bash
sudo mysql_secure_installation
```

&#x20;

Se le preguntará si desea configurar el `VALIDATE PASSWORD PLUGIN`.

{% hint style="info" %}
La habilitación de esta característica queda a discreción del usuario. Si se habilita, MySQL rechazará con un mensaje de error las contraseñas que no coincidan con los criterios especificados. Dejar la validación desactivada será una opción segura, pero siempre deberá utilizar contraseñas seguras y únicas para credenciales de bases de datos.
{% endhint %}



Elija `Y` para indicar que sí, o cualquier otra cosa para continuar sin la habilitación.

```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
```

Si responde “sí”, se le solicitará que seleccione un nivel de validación de contraseña. Tenga en cuenta que, si ingresa `2` para indicar el nivel más seguro, recibirá mensajes de error al intentar establecer cualquier contraseña que no contenga números, letras en mayúscula y minúscula, y caracteres especiales, o que se base en palabras comunes del diccionario.

```
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```

Independientemente de que haya elegido instalar el `VALIDATE PASSWORD PLUGIN`, su servidor le solicitará, a continuación, que seleccione y confirme una contraseña para el **root** user de MySQL. No debe confundirse con el **root del sistema**. El **root user de base de datos** es un usuario administrativo con privilegios completos sobre el sistema de base de datos. Si bien el método de autenticación predeterminado del root user de MySQL no requiere el uso de una contraseña, **incluso si hay una establecida**, deberá definir una contraseña segura en este punto como una medida de seguridad adicional. Hablaremos de esto en breve.

Si habilitó la validación de contraseña, se le indicará la seguridad de la contraseña del root user que acaba de ingresar y su servidor le preguntará si desea continuar usándola. Si está conforme con su contraseña actual, ingrese `Y` para indicar “sí” en la solicitud:

```
Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
```

Para el resto de las preguntas, presione `Y` y `ENTER` en cada mensaje. Con esto, se eliminarán algunos usuarios anónimos y la base de datos de prueba, se deshabilitarán las credenciales de inicio de sesión remoto de root y se cargarán estas nuevas reglas para que MySQL aplique de inmediato los cambios que realizó.

Cuando termine, compruebe si puede iniciar sesión en la consola de MySQL al escribir lo siguiente:

```bash
sudo mysql
```

&#x20;

Esto permitirá establecer conexión con el servidor de MySQL como **root** user de la base de datos administrativa, lo que se infiere del uso de `sudo` cuando se ejecuta este comando. Debería ver el siguiente resultado:

```
OutputWelcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 22
Server version: 8.0.19-0ubuntu5 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

Para salir de la consola de MySQL, escriba lo siguiente:

```bash
exit
```

&#x20;

Observe que no necesitó proporcionar una contraseña para conectarse como **root** user, a pesar de que definió una al ejecutar la secuencia de comandos `mysql_secure_installation`. Esto se debe a que el método de autenticación predeterminado para el usuario administrativo de MySQL es `unix_socket` en vez de `password`. Si bien esto puede parecer un problema de seguridad inicialmente, hace que el servidor de la base de datos sea más seguro porque los únicos usuarios que pueden iniciar sesión como **root** user de My SQL son los usuarios del sistema con privilegios sudo que establecen conexión desde la consola o mediante una aplicación que se ejecute con los mismos privilegios. En términos prácticos, eso significa que no podrá usar el usuario **root** de la base de datos administrativa para establecer conexión desde su aplicación PHP. Establecer una contraseña para la cuenta **root** de MySQL es una medida de protección, en caso de que el método de autenticación predeterminado se cambie de `unix_socket` a `password`.

Para mayor seguridad, es mejor disponer de cuentas de usuario dedicadas con privilegios de menor alcance configurados para cada base de datos, en especial si planea disponer de varias bases de datos alojadas en su servidor.

{% hint style="info" %}
Al momento de la redacción de este artículo, la biblioteca PHP nativa de MySQL `mysqlnd` [no admite](https://www.php.net/manual/en/ref.pdo-mysql.php) `caching_sha2_authentication`, el método de autenticación predeterminado de MySQL 8. Por este motivo, al crear usuarios de bases de datos para aplicaciones PHP en MySQL 8, deberá asegurarse de que estén configurados para usar `mysql_native_password` en su lugar.
{% endhint %}
