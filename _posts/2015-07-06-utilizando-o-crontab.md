---
id: 172
title: Utilizando o Crontab
description: Utilizando o Crontab
date: 2015-07-06T15:45:15-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=172
permalink: /utilizando-o-crontab/
geo_public:
  - "0"
categories:
  - Linux
---
<table class=" alignleft mceItemTable" border="0" align="center">
  <tr>
    <td>
      Comando
    </td>
    
    <td>
      Função
    </td>
  </tr>
  
  <tr>
    <td>
      crontab -e
    </td>
    
    <td style="text-align:left;">
      Edita o crontab atual do usuário
    </td>
  </tr>
  
  <tr>
    <td>
      crontab -l
    </td>
    
    <td>
      Exibe o atual conteúdo do crontab do usuário
    </td>
  </tr>
  
  <tr>
    <td>
      crontab -r
    </td>
    
    <td>
      Remove o crontab do usuário
    </td>
  </tr>
</table>

<p style="text-align:left;">
  <p style="text-align:left;">
    <p style="text-align:left;">
      <p style="text-align:left;">
        A linha é dividida em 6 campos separados por tabs ou espaço:
      </p>
      
      <table class=" alignleft mceItemTable" border="0" align="center">
        <tr>
          <td>
            Campo
          </td>
          
          <td>
            Função
          </td>
        </tr>
        
        <tr>
          <td>
            1o.
          </td>
          
          <td>
            Minuto
          </td>
        </tr>
        
        <tr>
          <td>
            2o.
          </td>
          
          <td>
            Hora
          </td>
        </tr>
        
        <tr>
          <td>
            3o.
          </td>
          
          <td>
            Dia do mês
          </td>
        </tr>
        
        <tr>
          <td>
            4o.
          </td>
          
          <td>
            Mês
          </td>
        </tr>
        
        <tr>
          <td>
            5o.
          </td>
          
          <td>
            Dia da semana
          </td>
        </tr>
        
        <tr>
          <td>
            6o.
          </td>
          
          <td>
            Programa para execução
          </td>
        </tr>
      </table>
      
      <table class=" alignleft mceItemTable" border="0" align="center">
        <tr>
          <td>
            Campo
          </td>
          
          <td>
            Valores
          </td>
        </tr>
        
        <tr>
          <td>
            Minuto
          </td>
          
          <td>
            0-59
          </td>
        </tr>
        
        <tr>
          <td>
            Hora
          </td>
          
          <td>
            0-23
          </td>
        </tr>
        
        <tr>
          <td>
            Dia do mês
          </td>
          
          <td>
            1-31
          </td>
        </tr>
        
        <tr>
          <td>
            Mês
          </td>
          
          <td>
            1-12
          </td>
        </tr>
        
        <tr>
          <td>
            Dia da semana
          </td>
          
          <td>
            0-6 (o “0″ é domingo), 1 é segunda, etc.
          </td>
        </tr>
      </table>
      
      <p style="text-align:left;">
        <a style="line-height:1.5em;" href="http://www.devin.com.br/crontab/" target="_blank"><br /> </a>
      </p>
      
      <p style="text-align:left;">
        <p style="text-align:left;">
          <p style="text-align:left;">
            <p style="text-align:left;">
              <p style="text-align:left;">
                <p style="text-align:left;">
                  <a style="line-height:1.5em;" href="http://www.devin.com.br/crontab/" target="_blank">Fonte:</a>
                </p>