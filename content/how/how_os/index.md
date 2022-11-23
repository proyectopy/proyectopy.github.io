---
title: "HowTo | Parte 1 | Sistema operativo"
date: 2022-11-20T15:03:56+01:00
draft: false
description: "Explicamos como intalar el sistema operativo."
slug: "instalar-el-sistema-operativo"
tags: ["pi imager", "Raspberry", "Raspbian"]
series: ["Serie HowTo"]
series_order: 1
---

## Instalando Pi OS Lite 

Ya sabemos lo que es una Raspberry y tambien el equipamiento minimo para hacela funcionar, pero como todos estos aparatos no solo basta con enchufar a la corriente, tenemos que instaurarles un cerebro, lo que tecnicamente se llama instalarles el sistema operaticvo, hay muchas formas pero intentaré hacerlo de la forma más sencilla que yo se.

Puedes ver todos los articulos que componen esta serie [aquí](/how).

{{< alert >}}
**Te recordamos:** Existen una gran variedad de sistemas operativos, hay sistemas operativos estándar pero tambien hay algunos que consiguen  transformar tu Raspberry en una máquina de juego retro .
{{< /alert >}}

## Cual elegir
Antes de empezar quiero recordaros que este sistema operativo en el que me voy a basar este articulo es el oficial de la Raspberry.
En principio vamos a intalar el Raspberry Pi OS Lite 

> La versión "Lite" de Raspberry Pi OS no es una imagen mínima de Raspbian el Sistema operativo oficial de Raspberry Pi basada en la última versión de Debian . Esta imagen usa la línea de comandos en lugar de en un escritorio. 

Puedes ver todos las versiones de Raspberry Pi OS desde la pagina oficial de la rasperry Pi foundation accediendo desde [este enlace](https://www.raspberrypi.com/software/operating-systems/).

## Empecemos la faena. 

Vomo ya os he dicho, me baso en lo que yo considero yes solamente mi opinión `la forma más sencilla de hacerlo`. Oara empezar necesitaremos la tarjeta de memoria del [articulo anterior](/how/raspberry-lo-basico/) insertada en un lector y en un puerto USB de tu ordenador.

Ahora vamos a descargarnos un programa creado por la Raspberry Foundation que se llama Pi Imager desde [este enlace](https://downloads.raspberrypi.org/imager/imager_latest.exe), un enlace libre de virus ya que es el enlace oficial.

Una vez instalado lo ejecutamos y nos encontraremos con algo parecido a esto:

![Paso 1](/howto_OS/1.jpg)

Esta es la interfaz del programa en Windows que es el sistema operativo que uso.

El primer botón nos deja elegir el sistema operativo que queremos instalar y el segundo nos deja elegir la tarjeta. Una vez seleccionado qudará algo parecido a lo de la siguiente imagen.

![Paso 2](/howto_OS/2.jpg)

Ahora nos fijaremos en el botón con la rueda dentada que hay abajo, al pulsarlo nos abre una ventana en la que podremos elegir algunas opciones que nos facilitaran la vida para empezar a configurar nuestra Raspberry. Fijate en la imagen.

![Paso 3](/howto_OS/3.jpg)
Puedes elegir arriba del todo si quieres que la configuración sea para esta sesión o que el programa lo guarde para poder instalar el sistema operativo alguna que otra vez. `...Estoy casi seguro que te pasará...` aunque sigas esta guia.

Entre las opciones encontraras por este orden las siguientes:

```
Opción      	            Uso

set hostname	            Si lo seleccionas puedes elegir el nombre
                            que le asignarás al host si no eliges ningun
                            nombre se usará raspberri.local.
enable ssh	                Activa el acceso ssh a la Raspberry, necesario
                            en la version lite.
set username and pass	    Elije un nombre de usuario y una clave, si no le
                            asignas nombre el SO crea al usuario pi.
configure wireless LAN      Activa el WiFi, si no lo completas, en principio
                            solo podras conectarte por cable.
set locale settings         Elige el idioma a usar y la disposicion para el
                            teclado.

```

En esta imagen loo puedes ver mas claro

![Paso 4](/howto_OS/4.jpg)

Las opciones preseleccionadas yo siempre las he dejado por defecto y que te avise con un sonido al terminar yo nunca lo he usado, ya me dirás como suena si llegas a usarlo.

Guardas los cambios pulsando Save y al cerrar la ventana de las opciones, le das al boton que pone WRITE y espera un poco a que termine el proceso.

Una vez que termine ya tenemos el Raspberry Pi OS lite preparado para su primer arranque en tu Raspberry.

## Y eso es todo.

Ya solo falta extraer la tarjeta e insertarla en la Raspberry, enchufar el USB de la fuente de alimentación y esperar a que arranque.


En fin, el sistema operativo ya está en la micro SD y arrancando por primera vez tu Raspberry. Empezaremos a configurar la Raspberry en la `siguiente parte` de esta serie.


🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.


