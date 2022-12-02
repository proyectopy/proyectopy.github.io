---
title: "Tutos | Asignando a tu Raspberry Pi una ip estatica."
date: 2022-11-21T15:03:57+01:00
draft: false
description: "Los usuarios en la raspberry y configurar la ip que va a usar tu raspberry."
slug: "tutos-asignando-ip-estatica"
tags: ["configuracion", "ip", "DHCPCD", "daemon", "estatica"]
series: ["Tutoriales Basicos"]
series_order: 4
---

Te conectaste ya por primera vez a la raspberry, ya has usado a lo mejor por primera vez la consola de comandos, incluso un sistema operativo basado en linux.


Puedes ver todos los articulos que componen esta serie [aquí](/tutoriales).

## Poner la IP de tu raspberry estática.
Ya hemos averiguado como ver la ip que usa tu raspberry, pero eso no será lo más comodo para conectarte a tu raspberry, modificando solamente un archivo de tu raspberry, conseguiremos que siempre la raspberry utilice la misma IP eso se llama Ip estatica o fija. 

> Las IP's estáticas son direcciones únicas que se asignan a los dispositivod de una red. O sea, una dirección exacta que nunca se modifica.

{{< alert >}}
**Dirección IP rango:** La IP estática que configures la crearás copiando los tres primeros segmentos asignados que no cambian. Esos primeros tres segmentos identifican tu red y tu host. La ip estatica la puedes elegir tu, en el último segmentro eligiendo un numero que no coincida con ningun otro equipo de tu red.
{{< /alert >}}


Como dije antes para conectarse a la raspberry siempre en la misma IP deberemos editar un archivo que se llama dhcpcd.conf y que se encuentra en la ruta /etc, este archivo forma parte de un demonio, o servicio de sistema, que es son procesos de fondo que usa el sistema operativo.

Es el archivo de configuración del daemon del cliente DHCP que nos permite cambiar la IP privada de la raspberry y establecerla como fija, este daemon se puede usar como cliente DHCP (DHCPCD) para comunicarse con el router. 

Despues de todo este rollo, vamos a empezar por comprobar si tenemos activado DHCPCD, para ello abrimos la consola y nos conectamos como hicimos en el [anterior tutorial](/tutoriales/raspberry-primera-conexion/) y una vez conectado teclearemos los siguientes comandos:


```toml
sudo service dhcpcd status
```

Al ejecutar este comando obtendras un mensaje y en alguan parte del mismo encontrarás una linea que será aprecida a esta:

```
Active: inactive (dead) since Tue 2022-11-29 10:58:54 CET; 3s ago
```

Fijate en lo que pone y si es `active (running)` te puedes saltar este paso, si es `inactive (dead)`, debes ejecutar los sigientes comandos para activar el DHCPC

```toml
sudo service dhcpcd start
sudo systemctl enable dhcpcd
```

Ejecuta de nuevo... 

```toml
sudo service dhcpcd status
``` 
... y si todo lo has hecho bien ya debe aparecer `active (running)`

Ya hemos activado DHCPCD, ahora empezamos a editar su archivo de configuración **/etc/dhcpcd.conf** para hacer eso, el sistema operativo lleva integrado un editor de texto `se llama` nano `y es un editor de texto para linea de comandos`.

En nuestra terminal abriremos nuestro archivo con nano usando el siguiente comando:

<a name="nano"></a> 
```toml
sudo nano /etc/dhcpcd.conf
```

En la terminal aparecerá algo parecido a esto:

![Portable](/howto_config/nano.jpg)


Ya puedes empezar a modificar el archivo para asignar la IP fija, con las teclas de cursor del teclado, desplazate hasta el final del documento usando la flecha abajo y una vez posicionado alli escribe `interface eth0` si tu Raspberry está conectada por cable de red o `interface wlan0` si usa una red inalámbrica.
Una vez escrito lo que corresponda a tu situacion pulsa enter y en la siguiente linea escribirás `static ip_address=192.168.0.22/24` tomamos como ejemplo que tu equipo usa la mascara de subred `192.168.0` y que tu quieres situarte en el rango `22` en resumen que quieres usar la ip **192.168.0.22**.

{{< alert >}}
**Muy importante:** Asegurate de que la IP que estás configurando no la use ningún otro equipo de tu red.
{{< /alert >}}

Siguiendo con el ejemplo la ip de tu router que por resumir, es el que se encarga del reparto de IP's esta dentro de la mascara `192.168.0` y tiene asignado el rango `0` por lo que la ip del router será `192.168.0.0` por lo que en nuestro archivo en las siguientes lineas usaremos la dirección IPv4 del router `192.168.0.0` como puerto de enlace y servidor DNS. Por lo que escribiremos en el archivo `static routers=192.168.0.1` y  a continuación `static domain_name_servers=192.168.0.1 8.8.8.8`.

Puedes copiar los comandos como los pongo yo a continuación y pegarlos en tu archivo

```toml
interface eth0
static ip_address=192.168.0.22/24
static routers=192.168.0.0
static domain_name_servers=192.168.0.0 8.8.8.8
```

Recuerda adaptar las ips que introduzcas en el archivo para que coincidan las IPv4 que utiliza tu router y la que quieras usar tu en la Raspberry, asi como el interface dependiendo de tu tipo de conexión si es *cable o red*.

A continuacion pulsa `Ctrl + O` y despues `Enter`para guardar los cambios, y ahora debes cerrar el archivo pulsando `Ctrl + X`, ya tienes tu IP fija.

Reinicia la raspberri con elcomando 

```toml
sudo reboot
```

## Vayamos un poco mas allá.

Si posees conocimientos algo más avanzados puedes crear un script en bash queejecute los comandos haga todas las modificaciones por ti. 

Ya haré un tutorial de como hacerlo, `estoy trabajando en ello` pero a modo de avance para modificar el archivo y no usar **nano** deberemos incluir en el script lo siguiente:

```toml
#Asigna valores a las variables

ipadress="ip_elegida"
gateway="ip_del_router"
nservs="tus_nameservers"

#modifica el archivo /etc/dhcpcd.conf

sudo echo "# Añadido por el script de Configuracion" >> /etc/dhcpcd.conf
sudo echo "interface eth0" >> /etc/dhcpcd.conf
sudo echo "static ip_address=$ipadress/24" >> /etc/dhcpcd.conf
sudo echo "static routers=$gateway" >> /etc/dhcpcd.conf
sudo echo "static domain_name_servers=$gateway $nservs" >> /etc/dhcpcd.conf

```

## Y eso es todo.


Ya tienes tu ip fijay ya puedes conectarte a tu raspberry con la ip que has elegido y siempre la misma por muchas veces que la reinicies.

{{< alert "circle-info" >}}
**Poco a poco** voy ampliando los contenidos de esta web con más tutoriales, en breve podreis visitar tambien la seccion de tips, para acceder a tutoriales cortos en los que os explicaré por ejemplo y ya que ha salido en este tutorial, como crear scripts en bash para automatizar tareas.
Paciencia, ya que no dispongo de todo el tiempo que me gustaría para ampliar contenidos.
{{< /alert >}}

En la `siguiente parte` de esta serie activaremos al usuario root y cambiaremos la clave a tu usuario pi.

🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.

