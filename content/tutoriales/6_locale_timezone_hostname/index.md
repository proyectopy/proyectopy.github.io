---
title: "Tutos | Cambia hostname, idioma y la zona horaria "
date: 2022-12-01T17:03:57+01:00
draft: false
description: "En este tutorial vamos a cambiar la zona horaria el idioma y el hostname."
slug: "cambiar-zona-horaria-idioma-y-hostname"
tags: ["zona horaria", "idioma", "hostname", "locale", "nombres"]
series: ["Tutoriales Basicos"]
series_order: 6
---

Lo más probable es que tu consola emita los mensajes en inglés, no es nada preocupante, pero si puedes, por que no hacer que tu raspberry se comunique contigo en castellano ... o el idioma que elijas. 

Puedes ver todos los articulos que componen esta serie [aquí](/tutoriales).

## Hostname.
Hay cosas que tu Raspberry hace dependiendo de la hora y el dia que sea. Seguro que no querrias que la raspberry se reiniciara automaticamente si estás haciendo algo con ella.

> Una zona horaria o timezone es un área que usa  un horario estándar que coincide en todas las zonas que se hallan en esa timezone.

{{< alert "circle-info" >}}
**Personalizando:** Personalizar estos conceptos, no es algo obligatorio pero si aconsejable. es una ventaja que el idioma y el horario de tu Raspberry coincidan con el tuyo, y el hostname te facilitará acceder a ella desde tu red local.
{{< /alert >}}

Empecemos, conectate tu equipo a traves de [ssh](/tutoriales/raspberry-primera-conexion/#conectarse-a-la-raspberry) introduce tu usuario y su clave para acceder a la Raspberry.

Todas estas configuracions son sencillas de realizar un par de comandos son suficientes para hacerlo, para el hostname debemos modificar un par de archivos ambos se encuentran en al ruta `/etc/` los archivos a modificar son `/etc/hosts` y `/etc/hostname`.

Para modificar esos archivos puedes usar el editor `nano` y sustituir el nombre antiguo por el que tu elijas.


```toml
sudo nano /etc/hosts
```
y cambias el nombre de host que aparece por el que tu elijas. Guardas con `Ctrl + O` despues `Enter`, y cierras el archivo pulsando `Ctrl + X`.

```toml
sudo nano /etc/hostname
```
En este archivo haces lo mismo cambias el nombre de hostname que aparece por el que tu elijas. Guardas con `Ctrl + O` despues `Enter`, y cierras el archivo pulsando `Ctrl + X`.

Otra forma de hacerlo es, averiguar antes de nada el nombre de host que tiene ahora tu raspberry, para hacer eso escribe en la consola:

```toml
hostname
```

Anota el resultado, que es el actual nombre de tu hostname, y ejecuta en la consola los siguientes comandos cambiando `nombre-antiguo` por el resultado que has obtenido con el comando anterior y `nuevo_nombre` por el de tu elección :

```toml
sudo sed -i "s/nombre-antiguo/nuevo_nombre/g" /etc/hosts
sudo sed -i "s/nombre-antiguo/nuevo_nombre/g" /etc/hostname
```

Con esto sustituyes el hostname original por el nuevo nombre.

## Timezone.

Comprueba los valores que tienes en tu raspberry von el siguiente comando:

```toml
timedatectl
```

Este comando te muestra unos valores que en resumidas cuentas son estos:

- Local Time: La hora que tiene configurada tu Raspberry
- Universal Time: La hora UTC.
- RTC time: La hora del reloj de tiempo real. Normalmente coincidirá con UTC.
- Time zone: La zona horaria configurada. En mi caso Europe/Madrid (CET, +0100)
- System clock synchronized: informa de la sincronización del reloj del sistema con un servidor NTP.
- NTP service: Informa de si el servicio NTP de tu Raspberry está activo.
- RTC in local TZ: Informa de si el reloj en tiempo real está utilizando la hora local o UTC.

Ya tenemos los datos que necesitamos sobre la zona horaria, si quieres o tienes que cambiarlos, te dejo los comandos que necesitas para hacerlo.

```toml
sudo timedatectl set-timezone tu_zona_horaria
timedatectl
```

Solo debes sustituir `tu_zona_horaria` por tu timezone en mi caso Europe/Madrid. Puedes ver un listado completo de todas las timezones que admite tu raspberry ejecutando el siguiente comando:

```toml
timedatectl list-timezones | column
```

## Locale.

Si tu terminal te habla en inglés, este paso será el definitivo para que deje de hacerlo y te hable en tu idioma.

Normalmente si todo te sale en inglés es porque el idioma por defecto es ese pero asegurate usando este comando:

```toml
locale
```
Si al ejecutar esto te sale `LANG=en_GB.UTF` definitivamente podemos afirmar que tenemos configurado el inglés por defecto. 

Vamos a solucionarlo y a obligar a tu Raspberry a que te hable en tu idioma, modificaremos un par de archivos para activar idiomas aparte del inglés, y poner el tuyo por defecto.

El primer archivo que tenemos que modificar es `locale.gen` que se encuentra en la ruta `/etc/locale.gen` lo abrimos con `nano` puedes repasar como en 
nuestra [tutorial de como asignar ip estática](/tutoriales/tutos-asignando-ip-estatica/#nano).


```toml
sudo nano /etc/locale.gen
```

Busca en el archivo el texto `# es_ES.UTF-8 UTF-8` y quitale la almohadilla del principio dejandolo así `es_ES.UTF-8 UTF-8`, Al quitar la almoadilla lo que haces es descomentar ese texto y el sistema operativo lo interpretará como un comando, etc. Puedes descomentar todos los idiomas que desees y una vez guardes el archivo `Ctrl + O` - `Enter` - `Ctrl + X` estarán accesibles para el sistema operativo.

Que ha fallado te preguntarás mi consola esta todavia hablando inglés...

Tenemos que modificar otro archivo todavía. El archivo en cuestión es `/etc/default/locale` aqui sustituirás, con [nano](/tutoriales/tutos-asignando-ip-estatica/#nano) por supuesto el texto que incluye y lo cambiarás por `LANG=es_ES.UTF-8` o el idioma que quieras usar por defecto.

```toml
sudo nano /etc/default/locale
```
Reinicias tu Raspberry y ya se comunica contigo en el idioma que hayas elegido por defecto.

```toml
sudo reboot
```

## Vayamos un poco mas allá.

Vamos a ir un poco más alla creando un script que haga todo eso por nosotros.

[Crea tu script](/ideas/ideas-tu-primer-script-bash/) con los comandos que te dejo a continuación ejecutalo coo ya has hecho en otras ocasiones y tu raspberry harás todo por ti.


```toml
# -------------------------------------------------------    
#                 Variables a utilizar                  *
# -------------------------------------------------------
#cambia true por false si no quieres que se ejecute

# Cambiar Locale y Timezone
conf_timezone=true

# Configuración del hostname
conf_hostname=true

# Estas variables las cambias a tu gusto
tz="Europe/Madrid"
lang="LANG=es_ES.UTF-8"
hostname=$(cat /etc/hostname)
nuevohost="proyectopy"

# -------------------------------------------------------
# Cambiar Locale y Timezone  REVISADO
# -------------------------------------------------------

if [ "$conf_timezone" = true ]; then
    
    echo "**************************************************************"
    echo "        Configurando la zona horaria y el idioma              "
    echo "**************************************************************"

    #modifica tu timezone donde pone Europe/Madrid en la siguente linea#
    sudo timedatectl set-timezone $tz
    timedatectl

    #modifica tu locale descomentando es_ES.UTF-8  
    sudo sed -i 's/^# *\(es_ES.UTF-8\)/\1/' /etc/locale.gen
    sudo locale-gen
    #modifica el archivo hostname cambiando el nuevo nombre
    sudo sed -i "s/LANG=en_GB.UTF-8/LANG=es_ES.UTF-8/g" /etc/default/locale

    sudo update-locale

    sleep 3

    else
    echo "**************************************************************"
    echo "  No vamos a configurar ahora la zona horaria y el idioma     "
    echo "**************************************************************"

    sleep 3

fi

# -------------------------------------------------------
# Configuracion del Hostname  REVISADO
# -------------------------------------------------------

if [ "$conf_hostname" = true ]; then

    echo "**************************************************************"
    echo "                Configurando el hostname                      "
    echo "             El hostname actual es $hostname                  "
    echo "**************************************************************"
    
    #modifica el archivo hosts cambiando el nuevo nombre
    sudo sed -i "s/$hostname/$nuevohost/g" /etc/hosts

    #modifica el archivo hostname cambiando el nuevo nombre
    sudo sed -i "s/$hostname/$nuevohost/g" /etc/hostname

    echo "**************************************************************"
    echo "               Se ha cambiado por $nuevohost                  "
    echo "**************************************************************"

    sleep 3

    else

    echo "**************************************************************"
    echo "          El hostname $hostname no se cambia ahora            "
    echo "**************************************************************"

    sleep 3

    sudo reboot

fi
```

## Y eso es todo.


Nos ha quedado un poco largo este tuto,pero como está separado por partes te lo puedes tomar con más o menos calma. 

{{< alert "circle-info" >}}
**Poco a poco** voy ampliando los contenidos de esta web con más tutoriales, ~~~~en breve podreis~~~~ ya podeis visitar tambien la seccion de [ideas](/ideas), con tutoriales cortos en los que mostraré como hacer cosas básicas.
{{< /alert >}}

En la `siguiente parte` de esta serie os explicaré como actualizar el sistema y como expandir el sistema de archivos para usar el 100% de tu tarjeta de memoria.

🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.

