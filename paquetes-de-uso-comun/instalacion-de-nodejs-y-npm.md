# Instalación de NodeJs y NPM

Para obtener esta versión, puede utilizar el administrador de paquetes `apt`. Actualice su índice de paquetes locales escribiendo primero lo siguiente:

```bash
sudo apt update
```

A continuación instale Node.js:

```bash
sudo apt install nodejs
```

Compruebe que la instalación se haya realizado de forma correcta haciendo una consulta a `node` sobre su número de versión:

```bash
nodejs -v
```

Si el paquete de los repositorios se ajusta a sus necesidades, será todo lo que necesita para configurar Node.js. En la mayoría de los casos, también le convendrá instalar `npm`, el administrador de paquetes de Node.js. Puede hacer esto instalando el paquete `npm` con `apt`:

```bash
sudo apt install npm
```
