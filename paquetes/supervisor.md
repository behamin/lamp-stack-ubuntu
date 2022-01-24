---
description: >-
  Supervisor es un sistema cliente / servidor que permite a sus usuarios
  monitorear y controlar una serie de procesos en los sistemas operativos UNIX.
---

# Supervisor

### Instalación

Comprueba que tu sistema base tiene los últimos paquetes disponibles:

```
apt-get update -y
```

De forma predeterminada, el paquete Supervisor está disponible en el repositorio predeterminado de Ubuntu 20.04. Puedes instalarlo con el siguiente comando:

```
apt-get install supervisor -y
```

Después de instalar Supervisor, puede verificar la versión instalada de Supervisor con el siguiente comando:

```
supervisord -v
4.1.0
```

### Configuración
