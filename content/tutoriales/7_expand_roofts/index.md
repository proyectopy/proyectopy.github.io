---
title: "Tutos | Expandir el sistema de archivos de la microSD"
date: 2022-12-01T17:03:57+01:00
draft: false
description: "En este tutorial vamos a aprovechar al máximo la tarjeta SD y actualizaremos el sistema."
slug: "expandir-sistema-de-archivos-microSD"
tags: ["update", "upgrade", "microSD", "actualizar", "roofts"]
series: ["Tutoriales Basicos"]
series_order: 7
---

La Raspberry puede funcionar con una microSD de muy poca capacidad pero ahora por muy pocos Euros podemos obtener tarjetas de memoria de gran capacidad por lo que podemos estar desaprovechando la mayoria de la capacidad de nuestra SD. 

Puedes ver todos los articulos que componen esta serie [aquí](/tutoriales).

## Expandir el sistema de archivos.

Cuando grabamos el SO en nuestra microSD te vas a dar cuenta de que solamente se aprovechan dependiendo del SO que uses un `par de Gigas` de tu tarjeta SD. Al instalar el SO, se crea automaticamente una una tabla de particiones predeterminada.
 
Hay muchas maneras de modificar esa tabla, pero los chicos de la [Raspberry Pi Foundation](https://www.raspberrypi.org/about/) han previsto esto y todas estas modificaciones se realizan desde la raspberry, usando la consola y al usuario root.


> Rootfs es una instancia especial de ramfs (o tmpfs, si está habilitado), que siempre está presente en los sistemas 2.6. No puede desmontar rootfs por aproximadamente la misma razón por la que no puede eliminar el proceso de inicio; en lugar de tener un código especial para verificar y manejar una lista vacía, es más pequeño y más simple para el kernel asegurarse de que ciertas listas no puedan quedar vacías. 
> - Fuente: https://www.kernel.org/doc/Documentation/filesystems/ramfs-rootfs-initramfs.txt.

{{< alert "circle-info" >}}
Raspbian ofrece una herramienta de configuración a traves de terminal, se trata de ***raspi-config***. Es una herramienta que se usa por terminal con un aspecto retro con una apariencia retro y unas funcionalidades poderosas.
{{< /alert >}}

En este caso, no voy a realizar esta configuración usando raspy-config, esta potente herramienta necesita un capitulo exclusivo para ella, casi todo lo que te he explicado en esta serie de tutoriales se puede hacer con ella. 

***Queda pendieente para un proximo tuto sobre el uso de raspi-config.***

Comprobemos nuestra tarjeta sd para ver como se encuentran repartido el sistema en nuestra tarjeta de memoria

```toml
sudo df -h
```
Dependera un poco del SO pero alejecutar tendremos algo parecido a esto:

```
S.ficheros      Tamaño  Usados  Disp    Uso%    Montado en 
/dev/root       1,2G    860M    246M    78%     / 
devtmpfs        459M    0       459M    0%      /dev
tmpfs           463M    0       463M    0%      /dev/temp 
tmpfs           463M    6,2M    457M    2%      /run 
tmpfs           5,0M    4,0K    5,0M    1%      /run/lock 
tmpfs           463M    0       463M    0%      /sys/fs/cgroup 
/dev/mmcblk0p1  60M     20M     41M     34%     /boot
```

El total que se esta usando es ínfimo comparandolo con los 64 Gb de capacidad de la SD que hay inserada en la raspberry.

Si en nuestra consola introducimos el comando que encontrareís despues de este párrafo, conseguiremos aprovechar todo el espacio de la SD.

```toml
sudo raspi-config --expand-rootfs
```

una vez ejecutado solo queda reiniciar la Raspberry.

Una vez reiniciada Comprobamos de nuevo nuestra tarjeta sd repitiendo el comando

```toml
sudo df -h
```
y si os fijais bien el espacio en la tarjeta ha variado
```
S.ficheros      Tamaño  Usados  Disp    Uso%    Montado en 
/dev/root       64G    861M     63G     5%     / 
devtmpfs        459M    0       459M    0%      /dev
tmpfs           463M    0       463M    0%      /dev/temp 
tmpfs           463M    6,2M    457M    2%      /run 
tmpfs           5,0M    4,0K    5,0M    1%      /run/lock 
tmpfs           463M    0       463M    0%      /sys/fs/cgroup 
/dev/mmcblk0p1  60M     20M     41M     34%     /boot
```

Una vez redimensionadas las particiones pasamos a lo siguente, actualizaremos el sitema 

## Vayamos un poco mas allá.

Y como ya es costumbre hagamos que la Raspberry haga todo el trabajo.

[Crea tu script](/ideas/ideas-tu-primer-script-bash/) con los comandos que te dejo a continuación ejecutalo como ya has hecho en otras ocasiones y tu raspberry harás todo por ti.


```toml
# -------------------------------------------------------    
#                 Variables a utilizar                  *
# -------------------------------------------------------
#cambia true por false si no quieres que se ejecute

# Expandir sistema de archivos
conf_expand=true


# Estas variables las cambias a tu gusto
# Este scipt no usa variables

# -------------------------------------------------------
# Expandir sistema de Archivos   REVISADO
# -------------------------------------------------------

if [ "$conf_expand" = true ]; then 

    echo "**************************************************************"
    echo "      Esto cambia el tamaño del sistema de archivos           "
    echo "**************************************************************"

    #Ejecuta el resize de la sd de la Raspberry
    sudo raspi-config --expand-rootfs

    echo "**************************************************************"
    echo "    Hemos aprovechado al maximo la tarjeta SD o el HDD        "
    echo "  Pero no tendrá efectos hasta que reinicies el sistema       "
    echo "**************************************************************"
    
    sleep 3
    else

    echo "**************************************************************"
    echo "     Las particiones de la SD o HDD no han variado            "
    echo "**************************************************************"

    sleep 3
fi
```

## Y eso es todo.
Bueno, ptera cosa aprendida, espero que todo este `rollo` os esté sirviendo, para eso lo hago desde luego. 

{{< alert "circle-info" >}}
**Poco a poco** voy ampliando los contenidos de esta web con más tutoriales, ~~~~en breve podreis~~~~ ya podeis visitar tambien la seccion de [ideas](/ideas), con tutoriales cortos en los que mostraré como hacer cosas básicas.
{{< /alert >}}

En la `siguiente parte` de esta serie os explicaré como poder automatizar la actualización del sistema.

🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.

