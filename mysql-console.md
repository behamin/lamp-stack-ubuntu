---
description: Lista de comandos más utilizados en MYSQL
---

# MYSQL console

Acceder

```
 mysql -u USER -pPASSWORD
```

Crear un nuevo usuario

```
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
```

Permisos a un usuario

```
GRANT ALL PRIVILEGES ON * . * TO 'user'@'localhost'; or
GRANT ALL PRIVILEGES ON database_name.* TO 'user'@'localhost';
FLUSH PRIVILEGES;
```

Revocar permisos

```
REVOKE PERMISSION_TYPE ON database_name.table_name FROM ‘user’@‘localhost’;
```

Posicionarte en una base de datos

```
 USE gesforcon;
```

Mostrar las tablas

```
SHOW TABLES;
```
