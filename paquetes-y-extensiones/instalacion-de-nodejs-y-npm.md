# Instalación de NodeJs y NPM

Antes de canalizar el comando mediante `bash`, siempre es recomendable revisar la secuencia de comandos para asegurarse de que no haga nada que no desee. Puede hacerlo eliminando el segmento de `| bash` al final del comando `curl`:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh
```

Revíselo y asegúrese de estar cómodo con los cambios que realiza. Cuando esté satisfecho, ejecute el comando de nuevo con `| bash` anexado al final. La URL que utilice cambiará en función de la última versión de NVM, pero ahora la secuencia de comandos se puede descargar y ejecutar escribiendo lo siguiente:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

Esto instalará la secuencia de comandos `nvm` en su cuenta de usuario. Para usarlo, primero, debe obtener su archivo `.bashrc`:

```bash
source ~/.bashrc
```

Ahora, puede preguntar a NVM qué versiones de Node hay disponibles:

```bash
nvm list-remote
```

```
Output. . .
       v12.13.0   (LTS: Erbium)
       v12.13.1   (LTS: Erbium)
       v12.14.0   (LTS: Erbium)
       v12.14.1   (LTS: Erbium)
       v12.15.0   (LTS: Erbium)
       v12.16.0   (LTS: Erbium)
       v12.16.1   (LTS: Erbium)
       v12.16.2   (LTS: Erbium)
       v12.16.3   (Latest LTS: Erbium)
        v13.0.0
        v13.0.1
        v13.1.0
        v13.2.0
        v13.3.0
        v13.4.0
        v13.5.0
        v13.6.0
        v13.7.0
        v13.8.0
        v13.9.0
       v13.10.0
       v13.10.1
       v13.11.0
       v13.12.0
       v13.13.0
       v13.14.0
        v14.0.0
        v14.1.0
        v14.2.0
```

¡Es una lista muy larga! Puede instalar una versión de Node al escribir cualquiera de las versiones que vea. Por ejemplo, para obtener la versión v13.6.0, puede escribir lo siguiente:

```bash
nvm install v13.6.0
```
