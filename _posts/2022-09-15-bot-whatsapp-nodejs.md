---
layout: post
title:  "Crear bot para whatsapp con NodeJS y whatsapp-web.js"
author: kuatroestrellas
categories: [ nodejs, bots, whatsapp ]
image: assets/images/bot-nodejs.jpg
description: "Crear bot para whatsapp con la libreria whatsapp-web.js y NodeJS"
---
En este tutorial crearemos un simple bot para whatsapp en unos minutos totalmente gratis

## Si vienes solo por el código da click [aquí](#code)

<p><iframe style="width:100%;" height="400" src="https://www.youtube.com/embed/Ks2UdXyYH_8?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>

Navegando por la deep web y la matrix me encontré con la libreria de [**whatsapp-web.js**](https://wwebjs.dev/guide/) y justo en ese momento necesitaba crear un bot para whatsapp, esta es una libreria para **nodeJS** que sirve para crear bots para whatsapp sin necesidad de usar la API oficial, ni plataformas de pago como Twilio, simula ser un cliente web que ejecuta la version web de whatsapp, se vincula igual por código QR.

Lo primero que haremos será preparar nuestro entorno de desarrollo, creamos la carpeta del proyecto y dentro de nuestra carpeta creamos un archivo llamado **index.js** (realmente pueden llamarlo como ustedes quieran solo asegurense de ponerle la extensión .js), una vez hecho esto abrimos nuestra terminal, simbolo de sistema o la consola que usen, nos situamos en la carpeta del proyecto y tecleamos el siguiente comando para instalar las dos librerias de nodejs que usaremos en este tutorial, **whatsapp-web.js** y **qrcode-terminal**, este último generará el qr para vincular whatsapp a nuestro bot como si se tratase de una conexion a whatsapp web normal:

```
npm i qrcode-terminal whatsapp-web.js
```

con esto se instalaran las librerias y una vez instaladas ya podemos programas nuestro bot, este bot será un simple hola mundo que nos responderá solamente cuando detecte el mensaje **"hola mundo"**.
<div id="code"></div>
El siguiente paso es pegar el siguiente código en nuestro index.js

<script src="https://gist.github.com/kuatroestrellas/a127ac1d12c6ac83dafee3fe57281949.js"></script>

Como pueden ver el código es relativamente sencillo, Ver líneas 29-34, en esta parte del código es donde sucede la magia, aquí pondremos las condiciones, como esto es un simple bot le pondremos que al escribirle **hola mundo** responda con un:  
**Hola soy un bot, mi creador esta ocupado ayudando a gohan a salvar la tierra**

Ahora si todo a ido bien lo ejecutaremos por primera vez y nos mostrará un código QR que escanearemos desde nuestro teléfono en whatsapp para establecer la conexión

```
node index.js
```

![bot](https://i.imgur.com/LxrLirl.png)

Si nos muestra el mensaje de **Conexión exitosa nenes** significa que nuestro bot realmente funciona, ahora solo hay que probarlo, al numero que vinculamos al código qr le enviaremos el mensaje **hola mundo**, y nos debe responder el mensaje que hayamos escrito, en nuestro caso es: **Hola soy un bot, mi creador esta ocupado ayudando a gohan a salvar la tierra**

![bot whatsapp](https://i.imgur.com/NePqJDyh.png)

Funciona, nos compiló a la primera, tenemos un bot totalmente gratis y funcionando.

En el próximo tutorial vamos a crear un bot que nos redireccione los mensajes de whatsapp al chat de Google

Comenta si te funcionó o si te perdiste en algún paso, también que te gustaría que hicieramos con este bot.

Saludos

**#compilaalaprimera**