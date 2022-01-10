# Crear usuario administrador

El primer paso sería abrir la consola de mongo.

```
mongo
```

Una vez abierta, lanzamos el siguiente comando.

```
use admin
```

Escribimos lo siguiente.

```php
db.createUser(
    {
      user: "your_user",
      pwd: "your_pass",
      roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
    }
  )
```

Para comprobar si nuestro usuario se ha creado con éxito y lo tenemos listado podemos lanzar.

```
show users
```

