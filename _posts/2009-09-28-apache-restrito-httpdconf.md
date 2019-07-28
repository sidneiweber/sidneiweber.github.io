---
id: 19
title: Apache restrito httpd.conf
date: 2009-09-28T18:51:29-03:00
author: Sidnei Weber
layout: post
guid: http://clancpd.com.br/sidneiweber/?p=19
permalink: /apache-restrito-httpdconf/
categories:
  - Apache
---
\# Diretório Restrito

Options Indexes FollowSymLinks Includes  
AllowOverride AuthConfig

#Autenticao  
AuthName &#8220;Acesso ao SARG&#8221;  
AuthType Basic  
AuthBasicProvider &#8220;ldap&#8221;  
AuthLDAPURL &#8220;ldap://201.7.197.39:389/dc=topazio,dc=com?uid?sub&#8221;  
authzldapauthoritative Off  
#AuthUserfile /etc/apache2/apache_passwd  
require user sweber  
#AuthUserfile /etc/apache2/apache_passwd  
#require valid-user

Order allow,deny  
Allow from all

\# Diretorio Install

Options Indexes FollowSymLinks Includes  
AllowOverride AuthConfig

AuthName &#8220;Acesso ao INSTALL&#8221;  
AuthType Basic  
AuthBasicProvider &#8220;ldap&#8221;  
AuthLDAPURL &#8220;ldap://201.7.197.39:389/dc=topazio,dc=com?uid?sub&#8221;  
authzldapauthoritative Off  
#AuthUserfile /etc/apache2/apache_passwd  
require user sweber

Order allow,deny  
Allow from all