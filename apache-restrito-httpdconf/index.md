# Apache Restrito Httpd.conf

Exemplo de como restringir o acesso com apache realizando autenticação no LDAP.

# Diretório Restrito

```bash
Options Indexes FollowSymLinks Includes  
AllowOverride AuthConfig

#Autenticao  
AuthName &#34;Acesso ao SARG&#34;
AuthType Basic  
AuthBasicProvider &#34;ldap&#34;
AuthLDAPURL &#34;ldap://201.7.197.39:389/dc=topazio,dc=com?uid?sub&#34;
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

AuthName &#34;Acesso ao INSTALL&#34;
AuthType Basic  
AuthBasicProvider &#34;ldap&#34;
AuthLDAPURL &#34;ldap://201.7.197.39:389/dc=topazio,dc=com?uid?sub&#34;
authzldapauthoritative Off  
#AuthUserfile /etc/apache2/apache_passwd  
require user sweber

Order allow,deny  
Allow from all
```


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/apache-restrito-httpdconf/  

