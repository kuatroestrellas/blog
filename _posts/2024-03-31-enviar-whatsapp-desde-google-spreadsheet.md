---
layout: post
title:  "Mensajes de whatsapp desde Google Sheets"
author: kuatroestrellas
categories: [ Spreadsheet, bots, whatsapp, Apps Script ]
image: assets/images/google-sheets-whatsapp.png
description: ""
featured: True
---

## Saludos terricolas  
En este post vamos a automatizar nuestra hoja de Google Spreadsheet(Excel de google) para que envíe mensajes a nuestro numero de whatsapp.
La logica será la iguiente, tendremos dos columnas, la primera va a tener el mensaje y la segunda un botón que enviará el mensaje.

### Ya se la saben, si solo vienes por el código da click [aquí](#code)

Lo primero que tendremos que hacer crear una nueva hoja de Google, crearemos dos columnas: la primera será __MENSAJE__ y la segunda __ENVIAR__  
Seleccionamos la columna B y nos vamos al menú donde dice __Datos__ >> __Validación de datos__ >> __Añadir regla__  
En el primer campo donde dice Aplicar intervalo nos aparece 'Hoja 1'!B1:B1000, lo sustituimos por 'Hoja 1'!B2:B1000 para que la validación no se aplique a la casilla __ENVIAR__.  
En Criterios seleccionamos __Casilla__ >> Activamos la casilla de "Usar valores personalizados" :  
__Marcada: SI__  
__Desmarcada: NO__  
Click en __Hecho__ y listo.  
![validar](https://imgur.com/3qq6uMT.png)

Listo ahora en la columna B debemos de tener puras casillas de verificación, es todo lo que debemos hacer del excel(Google sheet).

### Ahora activaremos nuestra API para poder enviar mensajes a whatsapp
Para esto usaremos una plataforma gratuita llamada [CallMeBot](https://www.callmebot.com/blog/free-api-whatsapp-messages/)  
Debemos obtener la clave API del bot antes de usar la API:

1. Añade el número de teléfono +34 644 05 92 17 en Contactos de Teléfono. (Nómbralo como desees)
2. Envía este mensaje "__I allow callmebot to send me messages__" al nuevo Contacto creado (usando WhatsApp por supuesto)
3. Espere hasta recibir el mensaje "API Activated for your phone number. Your APIKEY is 123123" del bot.
Nota: Si no recibes la ApiKey en 2 minutos, inténtalo nuevamente después de 24hs.
4. El mensaje de WhatsApp del bot contendrá la apikey necesaria para enviar mensajes utilizando la API.

![callmebot](https://www.callmebot.com/wp-content/uploads/2020/04/allow-callmebot-e1590102959978-1024x240.jpg)

### El siguiente paso es automatizar nuestra hoja de Google Sheet, para esto vamos a utilizar Apps Script
Nos vamos a Extensiones >> Apps Script, borramos todo el codigo que nos aparezca y vamos a pegar el siguiente código:

<div id="code"></div>
<script src="https://gist.github.com/kuatroestrellas/22867ed5b3fc92ccc04f23c4be1e0399.js"></script>

En las lineas 5 y 7 colocamos nuestro numero de whatsapp(nuestro numero) y la apikey que nos proporcionó CallMeBot.

__Guardamos__ y en esta misma pestaña de Apps Script nos vamos al menu lateral izquierdo donde dice __Activadores__, Seleccionamos __+ Añadir activador__, dejamos todo como en la siguiente imagen:

![Imgur](https://imgur.com/JKcW79V.png)

La función a ejecutar será __onEdit__, despliegue Principal, la fuente del evento elegimos __De una hoja de calculo__, y en tipo de evento seleccionamos __Al editarse__  
### Guardar y nos va a pedir ciertos permisos, autorizamos y listo
Nos aseguramos de guardar todo el script y regresamos a la pestaña de la Hoja de calculo, recargamos la página, se deberá cerrar la pestaña de apps script, y si todo está correctamente hecho ya debe funcionar nuestra hoja.

__Ahora__ simplemente escribimos en la columna __mensaje__, marcamos la casilla __enviar__ y al momento el numero de CallMeBot nos debe enviar ese mismo mensaje a nuestro whatsapp.

![captura](https://imgur.com/7sm4GNb.png)


Aqui dejo un video por si te trabaste en algun paso.

<p><iframe style="width:100%;" height="400" src="https://www.youtube.com/embed/jh5-Cc39ovc?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>

# Saludos, hasta la próxima!!