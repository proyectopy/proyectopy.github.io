---
title: "Tutos | Primera conexion a tu Raspberry"
date: 2022-11-21T15:03:56+01:00
draft: false
description: "Accediendo a la Raspberry por primera vez."
slug: "raspberry-primera-conexion"
tags: ["acceso", "usuarios", "root", "pi", "ip"]
series: ["Tutoriales Basicos"]
series_order: 3
---

Ya tienes una tarjetita metida en la raspberry, y deseando empezar, pero faltan algunos pasos, asi que no te desesperes, que todo llega.


Puedes ver todos los articulos que componen esta serie [aquí](/tutoriales).

## Direccion IP de tu raspberry
Lo primero que debemos averiguar es la dirección IP que usa tu Raspberry. Como siempre, averiguar ese dato se puede hacer de varias maneras, pero yo te voy a guiar de una manera nada complicada

> Una IP es un numero que identifica desde que punto de Internet está conectado un dispositivo.

{{< alert >}}
**Advertencia:** Yo en este momento estoy utilizando Windows 11 y puede que varien las imagenes y las localizaciones en alguna medida pero con algo de paciencia no es complicado.
{{< /alert >}}

Para averiguar la IP usaremos una herramintas gratuita y que no precisa instacion que se llama `Advanced IP Scanner`, puedes descargarla de manera segura desde su [sitio web](https://www.advanced-ip-scanner.com/es/)

Una vez descargada ejecuta la aplicacion y sigue los pasos que te indica eligiendo en la primera pantalla el idioma y en la segunda si quieres o no instalarlo. 

![Portable](/howto_config/1.jpg)

Pulsas siguiente y en la pantalla que se abre explorar.

![Boton](/howto_config/2.jpg)

Una barra de progreso aparece abajo y empieza a listar los equipos conectados a tu red.

![Escanear](/howto_config/3.jpg)

Examina el listado y aparecerá en alguna parte tu raspberry y su ip anotala que te hará falta.

![Listado](/howto_config/4.jpg)

En mi caso la raspberry está conectada por cable `192.168.1.105` y por WiFi `192.168.1.106` con dos ips diferentes ... Ya te explicaré más adelante.


## Conectarse a la Raspberry.

Ya has conseguido la ip, ahora ya podemos acceder a la Raspberry y empezar la configuración. Para acceder necesitamos otro programita que nos conectará usando el protocolo ssh a la Raspberry. Como ya es sabido hay muchas aplicaciones que lo pueden hacer, uno de las más conocidos es PuTTY, pero yo uso mRemoteNG está basado en PuTTY y a mi me gusta más.

Te facilito los links de descarga oficiales y ya tu eliges

- Descargar [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) desde su sitio oficial.
- Descargar [mRemoteNG Portable](https://github.com/mRemoteNG/mRemoteNG/releases/download/v1.76.20/mRemoteNG-Portable-1.76.20.24669.zip) desde su sitio oficial.
- Descargar [mRemoteNG Instalador windows](https://github.com/mRemoteNG/mRemoteNG/releases/download/v1.76.20/mRemoteNG-Installer-1.76.20.24615.msi) desde su sitio oficial.

En este articulo usaré mRemote, pero si eliges PuTTY no hay mucha diferencia.

Al abrir el programa, arriba aparece un cuadro como el de la siguiente imagen o similar. 

![Conexion ssh](/howto_config/5.jpg)

Fijate en la imagen y arriba, bajo el menu encuentras un cuadro donde introducirás tu IP, junto al cuadro hay una flecha señalando un desplegable donde elegiras la opcion SSH2. Introduce la IP, pulsa el botón.
Te aparecerá un mensaje diciendo `login as:` donde introducirás pi o el usuario que creaste en la configuracion de Pi Imager cuando grabaste el SO en la tarjeta SD. Escribe el usuario y te aparecera el mensaje `pi@192.168.1.xxx's password:` introduce la contraseña que elegiste, no te preocupes que parece que no escribe nada pero si lo hace.

Si todo es correcto te saldran alguna lineas con datos la fecha y por último el sigiente texto `pi@proyectopi:~ $` eso si cambiando proyectopi por tu nombre de host y un prompt para que empieces a teclear.


## Y eso es todo.

Ya estás conectado a tu Raspberry, ya podemos empezar a configurar la ip te diré como hacer para ponerla estatica y que no cambie cada vez que apagues el equipo.Tambien te dire como cambiar la contraseña, como activar y desactivar el usuario root (un usuario con permisos especiales) que por defecto viene desactivado y algunas cosas básicas para seguir con el proceso perseguido que es montar un centro multimedia y servidor web y de archivos.

En mi caso siempre uso la linea de comandos, pero si no te sientes cómodo, veras como te acostumbras pronto, puedes instalar una interfaz gráfica a tu SO Lite. En algun post publicaré como hacerlo.
En la `siguiente parte` de esta serie empezaremos con la configuración en si.

🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.

