# Apache restrito httpd.conf

Exemplo de como restringir o acesso com apache realizando autenticação no LDAP.

# Diretório Restrito

```bash
Options Indexes FollowSymLinks Includes  
AllowOverride AuthConfig

#Autenticao  
AuthName "Acesso ao SARG"
AuthType Basic  
AuthBasicProvider "ldap"
AuthLDAPURL "ldap://201.7.197.39:389/dc=topazio,dc=com?uid?sub"
authzldapauthoritative Off  
#AuthUserfile /etc/apache2/apache_passwd  
require user sweber  
#AuthUserfile /etc/apache2/apache_passwd  
#require valid-user

Order allow,deny  
Allow from all
```

# Diretorio Install

```bash
Options Indexes FollowSymLinks Includes  
AllowOverride AuthConfig

AuthName "Acesso ao INSTALL"
AuthType Basic  
AuthBasicProvider "ldap"
AuthLDAPURL "ldap://201.7.197.39:389/dc=topazio,dc=com?uid?sub"
authzldapauthoritative Off  
#AuthUserfile /etc/apache2/apache_passwd  
require user sweber

Order allow,deny  
Allow from all
```


---

> Author: Sidnei Weber  
> URL: https://sidneiweber.com.br/apache-restrito-httpdconf/  

