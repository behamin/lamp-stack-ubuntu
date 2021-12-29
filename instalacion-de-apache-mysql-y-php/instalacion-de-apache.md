# Instalación de Apache

Instale Apache usando el administrador de paquetes de Ubuntu, `apt`:

```
sudo apt update
sudo apt install apache2
```

Una vez que la instalación se complete, deberá ajustar la configuración de su firewall para permitir tráfico HTTP y HTTPS. UFW tiene diferentes perfiles de aplicaciones que puede aprovechar para hacerlo. Para enumerar todos los perfiles de aplicaciones de UFW disponibles, puede ejecutar lo siguiente:

```context
sudo ufw app list
```

Verá un resultado como este:

```php
OutputAvailable applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
```

A continuación, explicamos cada uno de estos perfiles:

* **Apache**: este perfil abre solo el puerto `80` (tráfico web normal no cifrado).
* **Apache Full**: este perfil abre los puertos `80` (tráfico web normal no cifrado) y `443` (tráfico TLS/SSL cifrado).
* **Apache Secure**: este perfil abre solo el puerto `443` (tráfico TLS/SSL cifrado).

Por ahora, es mejor permitir conexiones únicamente en el puerto `80`, ya que se trata de una instalación nueva de Apache y todavía no tiene un certificado TLS/SSL configurado para permitir tráfico HTTPS en su servidor.

Para permitir tráfico únicamente en el puerto `80` utilice el perfil `Apache`:

```
sudo ufw allow in "Apache"
```

Puede verificar el cambio con lo siguiente:

```
sudo ufw status
```



```
OutputStatus: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                                
Apache                     ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)                    
Apache (v6)                ALLOW       Anywhere (v6)   
```



Ahora, se permite tráfico en el puerto `80` a través del firewall.

Puede realizar una verificación rápida para comprobar que todo se haya realizado según lo previsto dirigiéndose a la dirección IP pública de su servidor en su navegador web (consulte la nota de la siguiente sección para saber cuál es su dirección IP pública si no dispone de esta información):

```
http://your_server_ip
```

Verá la página web predeterminada de Apache para Ubuntu 20.04, que se encuentra allí para fines informativos y de prueba. Debería tener un aspecto similar a este:

![Página predeterminada de Apache para Ubuntu 20.04](https://assets.digitalocean.com/articles/how-to-install-lamp-ubuntu-18/small\_apache\_default\_1804.png)

Si ve esta página, su servidor web estará correctamente instalado y el acceso a él será posible a través de su firewall.
