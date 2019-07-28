---
id: 149
title: Proxy transparente
date: 2014-02-16T19:31:32-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=149
permalink: /proxy-transparente/
categories:
  - Firewall
  - Squid
---
Fazer com que todas as conexões passem pelo proxy

Criar o arquivo:

<pre>cd /etc/init.d
touch rc.firewall</pre>

Adicionar o código:

<pre>#! /bin/sh
# Limpando tabelas do iptables
iptables -F
iptables -t nat -F
iptables -t mangle -F

# Definição da rede local
rede_interna=”192.168.0.0/16”

# Habilitando encaminhamento de pacotes e outras opções
echo “1″ &gt; /proc/sys/net/ipv4/ip_forward
echo “1″ &gt; /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
echo “1″ &gt; /proc/sys/net/ipv4/icmp_echo_ignore_all

# Carregando modulos necessários para o iptables
/sbin/modprobe iptable_nat
/sbin/modprobe ip_tables
/sbin/modprobe ipt_state
/sbin/modprobe ip_conntrack
/sbin/modprobe ipt_multiport
/sbin/modprobe iptable_mangle

iptables -I PREROUTING -t nat -p tcp -s $rede_interna –dport 80 -j REDIRECT –to-port 3128

iptables -t nat -I POSTROUTING -s $rede_interna -j MASQUERADE

iptables -A FORWARD -s $rede_interna -d loginnet.passport.com -j REJECT</pre>

Permissao de execução

<pre>chmod +x rc.firewall</pre>

Cuide para que o firewall inicie automaticamente na próxima inicialialização:

<pre>update-rc.d rc.firewall defaults</pre>

<a href="http://www.asteriskdocs.com.br/blog/instalando-e-configurando-squid-transparente-no-gnulinux-debian-e-derivados/" target="_blank">Fonte</a>