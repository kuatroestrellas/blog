---
layout: post
title:  "Recibir mensajes de Whatsapp en Google Chat"
author: kuatroestrellas
categories: [ nodeJS, bots, whatsapp, google chat ]
image: assets/images/whatsapp-google-chat.jpg
description: ""
featured: True
---
En esta ocasión vamos a redirigir todos los mensajes de whatsapp a el chat de google utilizando un bot hecho en javascript con node.js

## Si vienes solo por el código da click [aquí](#code)

Hace mucho tiempo en un trabajé en una empresa X donde teníamos prohibido usar redes sociales, en pocas palabras estaba prohibido ingresar el celular(o cualquier dispositivo), hay empresas que se toman muy enserio la seguridad e integridad de los datos de sus clientes, la única forma de comunicarnos dentro de la empresa era mediante el chat de google Workspace, y no se podía recibir mensajes del exterior, solamente podiamos recibir llamadas mediante la extensión telefónica, y da la casualidad que yo vengo de la aldea de la niebla, un pueblo marginado en las montañas de Oaxaca donde no hay señal de celular, así que la forma de comunicarme con mi familia es por whatsapp.

Entonces se me ocurrió🤔 porque no redirigir los mensajes de whatsapp al chat de google, claro solo para algun mensaje de emergencia.

Y usar un número de whatsapp unicamente destinado a este fin, solo emergencias, para no saturar mi bandeja con mensajes irrelevantes.

En un tutorial anterior ya vimos como [crear un bot para whatsapp]({{site.baseurl}}/bot-whatsapp-nodejs/), en esta ocasión fusionaremos el codigo anterior con el código para enviar mensajes asícronos al chat de Google Workspace.

Lo primero que haremos será preparar nuestro entorno de desarrollo, necesitamos crear nuestra carpeta del proyecto, crear nuestro archivo index.js e instalar las librerias necesarias:

- Tener nodejs instalado, una cuenta en google(solo funciona con google **Workspace**, no cuentas normales), y obviamente una cuenta de whatsapp
- **node-fetch** //para enviar mensajes a google
- **whatsapp-web.js** //para captar los mensajes de whatsapp
- **qrcode-terminal** //necesario para la libreria whatsapp-web.js y poder vincular nuestro whatsapp a la aplicación

Primero nos vamos a Google chat y crearemos un espacio, o también podemos situarnos en algun chat ya existente y seleccionar **Integraciones y apps**:
![imagen1](https://imgur.com/zix8p4c.png)

**Administrar webhooks**:
![imagen2](https://imgur.com/8yPCleX.png)

Le ponemos cualquier nombre a nuestro webhook y guardamos la URL que nos genera.

A continuación instalaremos las librerias necesarias:
```
npm i node-fetch@2.6.1
npm i qrcode-terminal whatsapp-web.js
```

Una vez instalado crearemos un archivo llamado index.js y agregamos el siguiente código:
<div id="code"></div>
<script src="https://gist.github.com/kuatroestrellas/5185647e43e682e8853c7fa12314a061.js"></script>

Ahora ejecutamos nuestro archivo, nos vamos a terminal y ejecutamos:

```
node index.js
```

Al ser la primera vez nos pedirá vincular nuestro whatsapp mediante un código QR al estilo whatsapp-web, y una vez vinculado los mensajes que recibamos se reenviaran automaticamente al chat de Google.

Y eso es todo, como puedes ver hemos hecho esto con unas cuantas líneas de código, espero y te haya funcionado a la primera, y si no, hazme saber tus dudas aquí abajo en los comentarios, también puedes sugerir que otro tutorial te gustaría que hiciera.

Aqui dejo un video paso a paso:

<p><iframe style="width:100%;" height="400" src="https://www.youtube.com/embed/aNy7Kyer3wU?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>

**Saludos!!**