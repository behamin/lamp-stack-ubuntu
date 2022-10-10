# LDAP

Para instalar y habilitar LDAP

```
sudo apt-get install php-ldap
sudo service apache2 restart
```

Si al intentar un login contra LDAP en un servidor te retorna el siguiente error:

<pre><code>Can't contact LDAP server
//Solución
<strong>sudo setsebool -P httpd_can_network_connect 1</strong></code></pre>

