---
id: 721
title: Instalando última versão do Ansible no Ubuntu/Debian
date: 2019-01-22T12:54:16-03:00
author: Sidnei Weber
layout: post
guid: https://sidneiweber.com.br/?p=721
permalink: /instalando-ultima-versao-ansible-no-ubuntu-debian/
img: "/ansible_ubuntu.png"
categories:
  - Ansible
  - Debian
  - Linux
  - Ubuntu
tags:
  - instalando ansible
---
Caso não saiba o que é Ansible, pode dar uma lida <a href="https://sidneiweber.com.br/2018/06/19/ansible-o-que-e-e-para-que-serve/" target="_blank">nesse post.</a>

A forma mais simples para instalar o Ansible é com o comando abaixo, porém é instalado uma versão mais antiga.

```shell
sudo apt-get update
sudo apt-get install ansible
```

Agora para baixar uma versão mais atualizada basta seguir os passos abaixo:

```shell
sudo aptitude update
sudo aptitude install python-pip
sudo pip install ansible
```
