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
