# MongoBD

Instalamos el módulo:

```
sudo pecl install mongodb
```

Necesitamos decirle a PHP que cargue la extensión **mongodb**.

```
sudo echo extension=mongodb.so > /etc/php/7.4/apache2/conf.d/30-mongodb.ini
sudo echo extension=mongodb.so > /etc/php/7.4/cli/conf.d/30-mongodb.ini
```
