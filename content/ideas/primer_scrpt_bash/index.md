---
title: "Ideas | Crear tu primer Script en bash"
date: 2022-11-29T11:03:56+01:00
draft: false
showTableOfContents : false
description: "Aprende a crear un script en bash."
slug: "ideas-tu-primer-script-bash"
tags: ["programacion", "automatizar", "scripts", "lenguajes", "bash"]
---

Este primer articulo , quiero incluieloo en una sección que he decidido llamar ideas, Los articulos de esta sección, pretendo que sean articulos cortos con conceptos y necesidades básicas para complementar los tutoriales y el resto de las secciones del sitio.


Puedes ver todas las ideas que se me van ocurriendo [aquí](/ideas).

## Bash y scripts que son.
Aunque pretendo que las ideas de esta sección sean articulos lo mas cortos posibles necesitamos unas bases para saber lo que vamos a hacer o decir. 

> Un script en pocas palabras es un sencillo programa que interpreta los comandos que se han integrado ordenadamente.

> Bash (Bourne-Again Shell) es un lenguaje de programación integrado de Unix que se usa para programar los scripts

{{< alert >}}
**Información:** Los datos y definiciones que aparecen aqui están basadas en datos recopilados en varios sitios de internet. El resto esta basado en mis experiencias, fallos y aciertos configurando mi Raspberry.
{{< /alert >}}

Para crear un script necesitamos un **editor de texto externo** o uno que esté incluido en el sistema operativo de la raspberry. es este ejemplo usaremos **nano**, pero vale cualquier otro.

Un script es un archivo de texto con extensión *.sh para crear nuestro primer script nos dirigiremos a nuestra consola conectada a la Raspberry a traves de ssh y lo crearemos con los siguientes comandos:

```bash
sudo cd ~ 
sudo touch proyectopy.sh 
sudo chmod +x proyectopy.sh
sudo nano ~/proyectopy.sh
```
- La primera linea o comando te situa en el directorio principal del usuario pi
- El segundo comando crea un archivo vacio que llamaremos script.sh
- El tercero asigna permisos de ejecución al archivo.
- Y el último comando abre tu archivo con el editor nano.

Una vez en nano puedes empezar a crear tu script, te dejo a continuación un pequeño ejemplo para que copies y pegues en nano y veras que sorpresa.

```bash
#!/bin/bash 
# -*- ENCODING: UTF-8 -*-
sudo touch sorpresa.sh 
sudo chmod +x sorpresa.sh
sudo chmod 0777 sorpresa.sh
sudo echo '#!/bin/bash' >> sorpresa.sh
sudo echo '# -*- ENCODING: UTF-8 -*-' >> sorpresa.sh
sudo echo '# Escribe a partir de aqui los comandos de tu script'
```

Guardas cambios en nao y cierras el archivo como ya te explique en [este tutorial](/tutoriales/tutos-asignando-ip-estatica/#poner-la-ip-de-tu-raspberry-est%C3%A1tica).

Ahora, haz un listado de los archivos que hay en el directorio home de tu usuario y veras el archivo que acabamos de crear para eso escribe en tu consola `ls` y aparecerán todos los archivos que tengas en el directorio /home/pi y entre ellos `proyectopy.sh`.

Como ya lo creamos con permisos de ejecucuón ejecutarlo es tan sencillo como escribir en la terminal

```bash
./proyectopy.sh
```
Cuando lo hayas ejecutado, es cuando viene la sorpresa. Vuelve a ejecutar `ls` en la consola y fijate que además de `proyectopy.sh` tenemos un archivo llamado `sorpresa.sh` que es el que ha creado el script `proyectopy.sh`.

Esos scripts se van a acumular en tu raspberry por lo que es buena practica borrarlos despues hacer el ejercicio, si no has cambiado los nombres solo escribe:

```bash
sudo rm proyectopy.sh sorpresa.sh
```
Si has cambiado los nombres, ya sabes, usa los tuyos.

## Y eso es todo

Ya hemos creado nuestro primer script que crea otro script con un par de comandos, a partir de aquí solo hay que dejar volar la imaginación. y empezar cualquier script en bash escribiendo `#!/bin/bash`.

Esperemos que esta  `idea` te haya servido de algo. Te espero en la `siguiente idea`. Gracias por aprender conmigo.

🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.
