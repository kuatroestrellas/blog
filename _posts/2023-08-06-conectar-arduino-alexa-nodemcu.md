---
layout: post
title:  "Crea tus dispositivos inteligentes compatibles con Alexa usando Arduino Cloud y NodeMCU"
author: kuatroestrellas
categories: [ arduino, iot, alexa, nodemcu ]
image: assets/images/alexa-esp.png
description: "Conecta tu Arduino con Alexa y dale esteroides a tus proyectos"
featured: True
---
En esta ocasión os enseñaré a conectar su placa NodeMCU ESP8266 a Alexa por medio de Arduino Cloud.
Arduino ha creado una skill oficial para conectar sus proyectos con Alexa, es compatible con gran cantidad de Arduinos que cuentan con wifi o ethernet, sin embargo a mi parecer son algo costosos, por eso es que yo he optado por utilizar la famosa y barata placa NodeMCU ESP8266, anteriormente no se podía pero ahora ya se puede usar este hardware con Arduino Cloud.

## Y si no tienes un alexa compralo desde mi link de referido plis <a target="_blank" href="https://www.amazon.com.mx/gp/search?ie=UTF8&tag=kuatroestre01-20&linkCode=ur2&linkId=88922280b087d899a5af82fe2f572397&camp=1789&creative=9325&index=electronics&keywords=Alexa">Click aquí</a>

### Si vienes a copiar el código da click [aquí](#code)

<p><iframe style="width:100%;" height="400" src="https://www.youtube.com/embed/YSVoxUxyASw?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>

Tengo flojera así que haré esto lo más resumido posible, si te trabas en algún paso guiate en el video.

Primero haremos las siguientes conexiones:  
D6 -> pin positivo led1  
D7 -> pin positivo led2  
GND -> patas negativas leds

![diagrama](https://i.imgur.com/sPFZWPZ.png)

Ahora nos iremos a [Arduino Cloud cloud.arduino.cc](https://cloud.arduino.cc/home/){:target="_blank"}
Si es la primera vez que te registras probablemente tengas que Instalar el ArduinoCreateAgent que se descargará automaticamente.
Selecionamos IoT Cloud y nos vamos a la pestaña Devices -> ADD DEVICE -> Third party device

![1](https://i.imgur.com/moj2EjO.png)

Seleccionamos nuestro dispositivo, en mi caso uso la NodeMCU 1.0
![2](https://i.imgur.com/32h2UEy.png)

Le ponemos un nombre y enseguida nos mostrará el ID del dispositivo y la Secret KEY, debemos guardar esta KEY en un lugar seguro ya que es con la que vincularemos a nuestro dispositivo.

![3](https://i.imgur.com/6D7nBd3.png)


Ahora nos vamos a la pestaña THINGS -> CREATE THING

![4](https://i.imgur.com/FWIRglE.png)

Damos click en ASSOCIATE DEVICE y se nos mostrarán los dispositivos que hemos agregado previamente.

![5](https://i.imgur.com/3FG8jDQ.png)

A continuación damos click en Network y pondremos datos de nuestro WIFI, o del wifi donde se vaya a conectar la placa ESP8266, y en Secret KEY ponemos el KEY que se nos generó cuando vinculamos nuestro dispositivo.

![6](https://i.imgur.com/ZdoqphC.png)

Ahora damos click en ADD VARIABLE, le pondremos de nombre foco1, seleccionamos Alexa Compatible y buscamos entre la lista **Light**
![7](https://i.imgur.com/XXMZZ8o.png)

Lo demas lo dejamos así como la siguiente imagen.
![8](https://i.imgur.com/UjRU4rk.png)

Guardamos y ahora dentro de la misma pestaña THINGS nos vamos a loa pestaña Sketch, aquí es donde se colocará todo el código.
![Imgur](https://i.imgur.com/hdAQ5Qe.png)

<div id="code"></div>
Verificamos que se reconozca nuestra placa, borramos todo el código y pegamos lo siguiente:
<script src="https://gist.github.com/kuatroestrellas/c0963a975d681fa4ceb1577840d79040.js"></script>

Como pueden ver el código no tiene nada del otro mundo, ahora que hemos pegado el código damos en Verify and Upload.
Esperamos unos minutos en lo que carga el código a nuestra placa.

Ya casi terminamos, ahora nos vamos a la pestaña **DASHBOARD** -> ADD -> Switch
![9](https://i.imgur.com/LJn753D.png)

Le ponemos nombre y seleccionamos **Link Variable**, elegimos foco1, guardamos, y creamos otro switch para foco2.
![10](https://i.imgur.com/IwHmouT.png)

Y listo, hemos terminado nuestra primera parte, probamos que al activar el switch nuestros leds enciendan y apaguen y si hemos hecho todo correctamente debe funcionar.
![11](https://i.imgur.com/cnYU1cA.png)
![12](https://i.imgur.com/Dz2OLKHl.jpg)

## AHORA VAMOS CON LA SEGUNDA PARTE

Ya que todo del lado de Arduino IoT Cloud y nuestro hardware funcionan correctamente nos iremos a la Aplicación de Alexa -> Más -> Skills y juegos. Y buscamos Arduino.

![alexa](https://i.imgur.com/2Tlbob9l.jpg)

Seleccionamos la primera opción que se muestra en la imagen, verificamos que el creador sea Arduino LLC:  
![alexaapp](https://i.imgur.com/ubc4Z5Ll.jpg)

Instalamos la Skill y nos pedirá que inciemos sesión con las credenciales de nuestra cuenta de Arduino  
![arduino](https://i.imgur.com/HJC9dkBl.jpg)

A continuación empezará a buscar dispositivos, esto puede demorar unos minutos, si hemos hecho todo correctamente nos va a detectar dos dispositivos.  
![devices](https://i.imgur.com/AdnWstWl.jpg)

Ahora nos pedirá configurarlos, seguimos los pasos con foco 1 y 2 y listo prros  
![I](https://i.imgur.com/OLIaxsml.jpg)
![II](https://i.imgur.com/AKr4OD4l.jpg)

Ahora ya estan reconocidos en la app de Alexa  
![III](https://i.imgur.com/BZmbnMOl.jpg)

Por último el momento más esperado

### Alexa enciende foco 1

![Final](https://i.imgur.com/LFpHSzzl.jpg)

Eso es todo amigos, ahora si quieren pueden usar unos relevadores para que encienda focos reales, yo tengo los relays pero vivo en casa rentada con caseros muy culeys que no me dejan tocar el cuarto.

Si tienes alguna duda o ideas para más proyectos perrones dejalo en los comentarios

**Saludos**

