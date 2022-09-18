---
layout: post
title:  "Recibir mensajes de Whatsapp en Google Chat"
author: kuatroestrellas
categories: [ nodeJS, bots, whatsapp, google chat ]
image: assets/images/whatsapp-google-chat.jpg
description: ""
featured: True
---
En esta ocasión vamos a redirigir todos los mensajes de whatsapp a el chat de google mediante un simple bot usando javascript con node.js

Hace mucho tiempo en un trabajé en una empresa X donde teníamos prohibido usar redes sociales, en pocas palabras estaba prohibido ingresar el celular(o cualquier dispositivo), hay empresas que se toman muy enserio la seguridad e integridad de los datos de sus clientes, la única forma de comunicarnos dentro de la empresa era mediante el chat de google Workspace, y no se podía recibir mensajes del exterior, solamente podiamos recibir llamadas mediante la extensión telefónica, y da la casualidad que yo vengo de la aldea de la niebla, un pueblo marginado en las montañas de Oaxaca donde no hay señal de celular, así que la forma de comunicarme con mi familia es por whatsapp.

Entonces se me ocurrió🤔 porque no redirigir los mensajes de whatsapp al chat de google, claro solo para algun mensaje de emergencia.

Y usar un número de whatsapp unicamente destinado a este fin, solo emergencias, para no saturar mi bandeja con mensajes irrelevantes.

En un tutorial anterior ya vimos como [crear un bot para whatsapp]({{site.baseurl}}/bot-whatsapp-nodejs/), en esta ocasión fusionaremos el codigo anterior con el código para enviar mensajes asícronos al chat de Google Workspace.

Lo primero que haremos será preparar nuestro entorno de desarrollo, necesitamos crear nuestra carpeta del proyecto, crear nuestro archivo index.js e instalar las librerias necesarias:

- node-fetch //para enviar mensajes a google
- whatsapp-web.js //para captar los mensajes de whatsapp
- qrcode-terminal //necesario para la libreria whatsapp-web.js y poder vincular nuestro whatsapp a la aplicación

