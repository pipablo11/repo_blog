+++
date = '2026-02-02T19:41:15+01:00'
draft = true
title = 'Creación de un servicio VPN con Tailscale'
tags = ["tailscale","proxmox","ssh"]
+++

# Introducción

Tailscale es un software que nos permite la creación de túneles cifrados entre dispositivos actuando como una VPN. En este post se mostrará como **instalar Tailscale** en un dispositivo y como añadirlo a tu red Tailscale, como hacer que un dispositivo anuncie las direcciones de tu red local y como usar un nodo de tu red de Tailscale como VPN para acceder a servicios de Internet.

## Qué es Tailscale


Tailscale es bla bla bla

## Instalación de Tailscale

Instalar Tailscale es un proceso muy sencillo y adaptado para la mayoría de dispositivos (Android, Linux, Windows, mac...). Simplemente debes acceder a la dirección de descarga de la [página web oficial](https://tailscale.com/download/android) y elegir la opción de tu sistema operativo. 

Una vez instalado, se debe utilizar el comando:

`$tailscale up --ssh´ 


Este comando te proporcionará un link, simplemente se debe acceder al mismo e iniciar sesión con tu cuenta tailscale. Automáticamente, el dispositivo se añadirá a tu red.

### Instalación en contenedor de Proxmox

Proxmox por defecto crea sus contenedores sin privilegios
Tailscale debe acceder /dev/net/tun o algo así que requiere de ellos

Opción 1: Dar privilegios, poco segura
Opción 2: bla bla bla

## Exponer direcciones y Nodo de salida

explicar como crear un nodo que exponga direcciones y lo otro

## Utilizar un nodo para acceder a servicios de Internet

Podemos utilizar un nodo como puente para acceder a servicios en línea como si estuviesemos en nuestra casa. Esto viene bien para plataformas de streaming como Netflix por ejemplo, donde algunas tarifas solo permiten utilizar la plataforma en una unidad familiar o si tienes algún servicio como proxmox que nos muestra una interfaz web.

Para esto hay dos alternativas (probada solo 1), activar nodo en la red LAN como external node o utilizarlo como proxy

### Utilizar nodo como proxy

explicación ----- 

Para ello, nos conectaremos a ese nodo mediante ssh con el parámetro -D utilizado para habilitar el reenvío dinámico de puertos a nivel de aplciación:

$ssh -D 8080 <usuario>@<dirección_ip>

Esto nos permite decirle a nuestro dispositivo, todo lo que recibas por el puerto 8080 envialo por *dirección_ip*. 

Posteriormente, deberemos especificar a nuestro navegador que utilice este puerto. Para ello habilitaremos un proxy en ajustes>proxy de nuestro navegador y le diremos:

Host SOCKS: 127.0,0,1 Puerto 8080

bla bla bla




