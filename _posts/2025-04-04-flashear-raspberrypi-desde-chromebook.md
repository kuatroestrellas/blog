---
layout: post
title: "Cómo instalar el sistema operativo de Raspberry Pi desde una Chromebook"
author: kuatroestrellas
categories: [linux, raspberry-pi, chromebook]
image: assets/images/rpi-chrome.png
description: "Flashea RaspberrypiOs en tu sd rápido con tu Chromebook"
featured: True
---

Flashea Raspberry Pi OS en tu tarjeta SD rápido con tu Chromebook

En esta ocasión vamos a ver cómo instalar el sistema operativo de **Raspberry Pi** directamente desde una **Chromebook**, sin necesidad de usar una laptop con Windows, Mac o Linux. Aunque el instalador oficial no tiene soporte para Chrome OS, hay una forma muy sencilla de hacerlo gracias a unas herramientas integradas en el sistema.

---

## ¿Por qué hacerlo desde una Chromebook?

Puede que no tengas acceso a una computadora con otro sistema operativo, o simplemente quieras aprovechar tu Chromebook al máximo. Ese fue mi caso, y por eso te comparto esta solución que me funcionó perfectamente.

---

## Si no tienes una raspberry pi comprala desde este link please(tengo que pagar renta):
[Kit Raspberry Pi 4 2gb RAM 🔗](https://mercadolibre.com/sec/1tEeibT){:target="_blank"}  
[Kit Raspberry Pi 4 8gb RAM 🔗](https://mercadolibre.com/sec/1Wg8tPD){:target="_blank"}


Te dejo paso a paso en este post o puedes ver el video.
<p><iframe style="width:100%;" height="400" src="https://www.youtube.com/embed/bl0mPv4dCCQ?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>

### 1. Descarga el instalador de Raspberry Pi

Primero, vamos a la [página oficial de Raspberry Pi](https://www.raspberrypi.com/software/) y descargamos la versión para **Ubuntu** (ya que Chrome OS está basado en Linux).

Una vez descargado, deberías tener el archivo `.deb` listo para instalar.

---

### 2. Habilita el entorno Linux (Crostini)

Chrome OS permite ejecutar aplicaciones de Linux mediante un entorno llamado **Crostini**. Para activarlo:

- Abre el menú de tu Chromebook y busca **Terminal**.

![diagrama](https://i.imgur.com/5AxO3cq.png)
- Te aparecerá una opción que dice "Entorno de desarrollo de Linux". Haz clic en **Configurar**.
![img](https://i.imgur.com/eoKVOgp.png)
- Asigna un nombre si lo deseas, deja las opciones por defecto y presiona **Instalar**.
- Espera unos minutos mientras se instala la máquina virtual.

---

### 3. Instala el instalador de Raspberry Pi
Ve a tu carpeta de descargas y ejecuta **.deb** que descargaste en el paso 1, dale doble click siguiente siguiente.  
![img](https://i.imgur.com/Ml055G7.png)


### 5. Conecta tu tarjeta Micro SD
La maquina virtual Linux no va a reconocer tu tarjeta Micro SD, debes activar el acceso compartido.

- Ve a **Configuración** >  Entorno de Desarrollo de Linux > Administrador de dispositivos USB.

![img](https://i.imgur.com/ZrPmCWC.png)

- Activa la opción para compartir la Micro SD con el entorno Linux.

![img](https://i.imgur.com/u7qJI7M.png)

Listo

### 6. Instala el sistema operativo
Ve a la terminal y escribe 
```
rpi-imager --platform 'xcb'
```

![img](https://i.imgur.com/fXY59e4.png)

> es muy importante poner --platform ya que sin el el rpi-imager no funcionará correctamente

**Listo** ya solo configura el modelo de tu tarjeta, version de SO a instalar y selecciona tu tarjeta Micro SD
![img](https://i.imgur.com/FzjreoA.png)

- Configura las opciones como nombre de usuario y contraseña.

Guardar, Yes, espera a que termine de escribir la tarjeta.

¡Y listo! Ya tienes tu sistema operativo instalado desde tu Chromebook, Ahora solo conecta la Micro SD a la Rasperry y a usarla.

Conclusión
Aunque Chrome OS no está oficialmente soportado, con unos simples pasos puedes usar tu Chromebook para preparar una tarjeta Micro SD para Raspberry Pi sin problemas. ¡Espero que te haya servido!