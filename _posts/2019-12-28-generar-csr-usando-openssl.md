---
layout: post
title:  "Generar un CSR en Google Cloud"
author: kuatroestrellas
categories: [ google cloud ]
description: "Generación de una solicitud de firma de certificado (CSR) en los servicios de Google Cloud"
---
Generación de una solicitud de firma de certificado (CSR) en los servicios de Google Cloud

**Antes de solicitar un certificado SSL**, es necesario generar una Solicitud de firma de certificado (CSR).

Google Cloud Platform le permite generar una CSR (Certificate Signing Request, Solicitud de Firma de Certificado) utilizando **Google Cloud Shell** , la consola de línea de comandos integrada que proporciona acceso a los recursos de la nube directamente desde un navegador.

Se requiere tener un proyecto creado previamente para acceder a Cloud Shell. Puede ser creado desde el **IAM y administración** de área [aquí](https://console.cloud.google.com/project?_ga=1.216733855.869957752.1479794157) . Una vez que se crea el proyecto, Google Cloud Shell está disponible para usted.

Google Cloud Shell se puede activar usando el botón **Activar Google Cloud Shell** en la parte superior de la ventana:
![walking]({{site.baseurl}}/assets/images/gcloud.png)

Se abrirá una nueva sesión de Cloud Shell en la parte inferior de la ventana. De forma predeterminada, se ubicará en el directorio de inicio del usuario /home/user:

Google Cloud Shell admite el kit de herramientas **OpenSSL** que se puede usar para la generación de CSR.

Los pasos para generar una CSR en Cloud Shell son :

- Ejecuta el siguiente comando para crear la solicitud de Clave Privada y Solicitud de Firma de Certificado ( server.key y server.csr ).
* Para evitar más confusión, recomendamos reemplazar "ejemplo.com" en ejemplo.com.key y ejemplo.com.csr con el nombre de dominio real para el que se emitirá el certificado.
{% highlight bash %}
openssl req -new -newkey rsa: 2048 -nodes -keyout ejemplo.com.key -out ejemplo.com.csr
{% endhighlight %}
> No olvides remplazar __ejemplo.com__ con el nombre de tu dominio real

Ahora se te pedirá que ingreses los siguientes datos  utilizando solo símbolos alfanuméricos en inglés.
Para algunos campos habrá un valor predeterminado.
- **Nombre del país** (código de dos letras)	El formato de [código de país](https://www.iso.org/obp/ui/) de dos letras de la Organización Internacional para la Normalización (ISO)
- **Nombre del estado o provincia** (nombre completo)
- **Nombre de la localidad** (ciudad) No lo abrevies.
- **Nombre de la organización** (se puede usar NA)
- **Nombre de la unidad organizativa** (se puede usar NA)
- **Nombre común** ( nombre de dominio o subdominio que desea proteger. Es decir, ejemplo.com o &#42;.example.com para SSL Wilcard)
- **email**
- **Una contraseña de comprobación** Esto se debe dejar en blanco (solo toca intro).
- **Un nombre de compañía opcional** Esto se debe dejar en blanco (solo toca intro).

Una vez que se proporciona toda la información solicitada, tendrás dos archivos generados en el directorio actual: * .csr y * .key.

> El código de clave privada es esencial para la instalación del certificado, que se realizará "después" de que el certificado se active y se emita. Asegúrate de guardar el archivo de clave privada o moverlo al directorio donde puede ubicarse más fácilmente. El contenido del archivo es un bloque de código que comienza con "----- BEGIN PRIVATE KEY -----" y termina con "----- END PRIVATE KEY -----".

### Siguiente paso
Tu CSR ha sido creado. Abre **ejemplo.com.csr** en un editor de texto, copia y pega el contenido en el formulario de inscripción en línea cuando se te solicite.

