---
layout: post
title:  "Controlar Arduino desde Cortana"
author: kuatroestrellas
categories: [ IoT, arduino, blynk ]
image: assets/images/2post.jpg
description: "Controlar luces de arduino remotamente desde Cortana"
---
## HOLA CORTANA prende la luz  

Hola makers, en esta ocasión les traigo un tutorial para controlar lo que tu Arduino pueda controlar mediante comandos de voz con la asistente virtual **Cortana**. 

Cuando se me ocurrió hacer esto mi idea era usar el SDK de Cortana para crear una skill, luego correr un servidor local en node.js que esté escuchando las peticiones y se encargue de enviarlo al arduino, mediante johny-five o algo parecido, pero me encontre con **Blynk** y **IFTTT**, y si ya esta inventada la rueda pues hay que usarla. 

- [IFTTT](https://ifttt.com/) es la onda cuando se trata de automatizar acciones y tareas en Internet, es un servicio que nos facilita la vida por ejemplo poder subir a Twitter la misma foto que subiste a Facebook, y entre los servicios que integra está el del Asistente de Google y Cortana.  
- [Blynk](https://blynk.io/) es una plataforma que permite controlar tu placa Arduino, Rapsberry Pi, ESP8266, NodeMCU, etc desde cualquier parte del mundo mediante una app disponible para Android y iOS, te da la posibilidad de crear una interfaz gráfica de arrastrar y soltar.  

>En este proyecto usé un Arduino UNO y el puerto Serie porque soy un estudiante pobre y no tengo para una Rapsberry Pi o un NodeMCU, pero te recomiendo que si tienes una placa NodeMCU/ESP8266 la uses ya que es mucho más cómodo y fácil de usar y no dependerás de tener encendida tu PC todo el tiempo. tan pronto tenga una de esas placas hago un nuevo tutorial.

**Ingredientes:**
- Arduino UNO <icon class="fa fa-buy"></icon><a href="https://s.click.aliexpress.com/e/_dSAL5cl" target="_parent">Comprar en Aliexpress<icon class="fa fa-shopping-cart"></icon></a>
- LED o relevador
- Un celular [iOS](https://itunes.apple.com/us/app/blynk-iot-for-arduino-esp32/id808760481?mt=8) o [Android](https://play.google.com/store/apps/details?id=cc.blynk&hl=en_US) con [Blynk](https://blynk.io/) Instalado
- PC con Windows 
- [IFTTT](https://ifttt.com/) instalado en tu teléfono, también puedes usar la versión web.

<br>
## EMPEZANDO CON BLYNK

- Abrimos la app y le damos en Nuevo Proyecto:
![post 1](https://i.imgur.com/Ft2KRAs.png)


- Le ponemos cualquier nombre al proyecto, Seleccionamos **Arduino UNO**, Conexión **USB**, **CREAR**:
![post 2](https://i.imgur.com/QMZbWJv.png)

- Una vez creado blynk nos genera un token y lo envía por email, esta sera nuestra "llave" para poder conectar el arduino a blynk


- Ahora nos muestra un lienzo, tocamos cualquier parte de la pantalla y nos saldrá un menú, selecionamos **Button**:
![post 3](https://i.imgur.com/6iJoJwh.png)


- Lo arrastramos a la posición que queramos y le damos click, en OUTPUT Seleccionamos digital(En mi caso usare el pin 8 de arduino así que selecciono D8), cambiar PUSH por SWITCH y listo.
![post 4](https://i.imgur.com/QBwNhLT.png)
<!--<img src="https://i.imgur.com/QBwNhLT.png" width="65%" heigth="65%">-->

<br>
## Configurando el Arduino

Lo primero que necesitaremos será instalar la libreria para que Blynk funcione en Arduino, para esto vamos a Herramientas **>** Administrado de Bibliotecas, Escribir **blink** en el buscador y asegurarnos de elegir la última versión
![arduino 1](https://i.imgur.com/vgSDQtj.png)

Ahora cargamos el siguiente sketch, solo copia y pega lo siguiente, ustedes son expertos haciendo eso, solo coloca tu token que te genero la app Blynk en uno de los pasos anteriores.
<script src="https://gist.github.com/kuatroestrellas/197bfc071fb9c1ffa743447c82431bf6.js"></script>

El circuito es simplemente conectar un LED o relevador al pin 8 y listo.

Ahora debemos buscar la carpeta donde estan almacenadas las librerias de arduino, buscar Blynk/scripts, luego abrir esa ruta en CMD, así:
```
cd PATH_ARDUINO_LIBRARIES/Blynk/scripts
```
en mi caso es:
```
cd C:\Users\Arturo\Documents\Arduino\libraries\Blynk\scripts
```
Ahora debemos detectar en que puerto serie esta conectado nuestro ARDUINO, ahora escribimos en CMD
```
blynk-ser.bat -c COM10
```
Sustituye COM10 con tu puerto Serie no seas tan wey.  
Y listo ya debería estar funcionando
![cmd](https://i.imgur.com/6vMGeH1.jpg)
> El paso anterior se habría evitado con una conexión wifi, por ejemplo usando una Rapsberry Pi o un nodeMCU, es solo para activar la conexion a internet al puerto serie en el cual está conectado el arduino.

## Ahora ve a blynk en tu telefono y dale PLAY
![app blynk](https://i.imgur.com/xi4DcRq.png)
Si hiciste todo bien hasta ahora
en estos momentos deberías poder encender y apagar el LED.
![arduino](https://i.imgur.com/7NtJuql.jpg)

<br><br>
<a href="https://s.click.aliexpress.com/e/_dV13flB?bz=725*90" target="_parent"><img width="725" height="90" src="//ae01.alicdn.com/kf/He7c2914340344500beb9908b8e408559a.png"/></a>
<br>
## FELICIDADES hemos hecho la parte más díficil de este tutorial ahora lo que viene es de lo más sencillo

Ahora nos dirigimos a la app de [IFTTT](https://ifttt.com/) y presionamos **GET MORE**
![ifttt](https://i.imgur.com/41hYqzv.png)

Presiona símbolo **+**
![applet](https://i.imgur.com/m92BLe2.png)

Sellecciona **This**
![](https://i.imgur.com/TxP1ets.png)

Busca y Selecciona a Cortana
![cortana](https://i.imgur.com/tzEFqtz.png)

Ahora crearemos un disparador, lo único que necesitamos es detectar una palabra clave en este caso, **"enciende la luz"**, así que selecciona **Say a specific phrase** 
![phrase](https://i.imgur.com/3DJbFlf.png)

Ahora rellenamos los campos con lo siguiente, esto es a como tu lo prefieras, puedes ecoger cualquier otra frase
- **Whar do you want to say?** : enciende la luz
- **What's another way to say it?** : prende el foco
- **What do you want Cortanato say in response?** : Entendido, como tu ordenes amo y señor doctor profesor Patricio

![](https://i.imgur.com/RGkIooH.png)

Ahora click en **That**
![](https://i.imgur.com/ze8s8QW.png)

Busca y selecciona **webhooks**
![](https://i.imgur.com/jgjrDaH.png)

Make a web request
![](https://i.imgur.com/SwYTsr3.png)
<br><br>  
Antes del siguiente paso vamos a nuestro cmd y escribimos lo siguiente para averiguar la dirección IP de los servidores de blynk en tu país, solo escribe:
```
ping cloud.blynk.cc 
```
y copia la IP que te salga para el próximo paso, en mi país es 45.55.96.146
<br><br>
Ahora rellenamos con los siguientes datos
- **URL** : http://IP_BLYNK_PAIS/TU_BLYNK_TOKEN/update/D8, ejemplo: http://45.55.96.146/eGNyA0Rf7Qn92CENyKolr24c_J2UEvXt/update/D8
- **METHOD** : PUT
- **Content type** : aplicattion/json
- **Body** : ["1"]

![](https://i.imgur.com/dw2EToa.png)
  
Confirmamos y damos Finish

## Ahora haremos los mismos pasos pero para apagar el foco

- creamos un nuevo applet
- **+** this
- seleccionar cortana
  - **Whar do you want to say?** : apaga la luz la luz
  - **What's another way to say it?** : apaga el foco
  - **What do you want Cortanato say in response?** : Entendido, como tu ordenes amo y señor doctor profesor Patricio
- **+** that
- seleccionar webhooks, todo es igual al primer ejemplo solo se cambia el **1** por es **0** en body
  - **URL** : http://IP_BLYNK_PAIS/TU_BLYNK_TOKEN/update/D8, ejemplo: http://45.55.96.146/eGNyA0Rf7Qn92CENyKolr24c_J2UEvXt/update/D8
  - **METHOD** : PUT
  - **Content type** : aplicattion/json
  - **Body** : ["0"]

Finish y listo
Si hicieron todo correctamente simplemente diganle a cortana que Encienda la Luz  
Aqui les dejo un demo ya funcionando
<p><iframe style="width:100%;" height="315" src="https://www.youtube.com/embed/aeIdE9sBKDo?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>

Si tienes alguna duda hazmelo saber

## En nuestro próximo post haremos lo mismo pero desde el asistente de Google: OK Google enciende la luz