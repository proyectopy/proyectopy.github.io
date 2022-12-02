---
title: "Tutos | Activando usuario root y cambio de claves"
date: 2022-12-01T17:03:57+01:00
draft: false
description: "Activar acceso root y cambio de claves usuarios."
slug: "tutos-activando-usuario-root-cambio-claves"
tags: ["configuracion", "root", "claves", "contraseña", "usuarios"]
series: ["Tutoriales Basicos"]
series_order: 5
---

Tenemos localizable en la red a nuestra Raspberry pero, hay cosas que no puedes hacer sin los privilegios de superusuario por eso `debemos` trabajar un poquito.

Puedes ver todos los articulos que componen esta serie [aquí](/tutoriales).

## Cambiar la clave de usuario pi.
Empezaremos por lo más sencillo, si sigues esta serie de tutoriales, posiblemente ya hayas elegido antes de instalar el SO la clave del usuario pi, incluso hayas creado tu propio usuario.

> Cuando grabamos el SO en una microSD se crea un usuario y una contraseña, necesarios para poder empezar a usar la Raspberry. Se crean siempre y por defecto son, el usuario pi y la contraseña raspberry.

{{< alert "circle-info" >}}
**Usuario Root:** En el SO de la raspbery y en otros, el superusuario o root es el nombre del usuario que posee todos los Privilegios. digamos que es la cuenta de administrador. El usuario pi puede actuar con privilegios root usando el comando `su`, pero si root no tiene asignada una clave, habrán comandos que no podrá ejecutar.  
{{< /alert >}}

Manos a la obra, accede a traves de [ssh](/tutoriales/raspberry-primera-conexion/#conectarse-a-la-raspberry) introduce tu usuario y su clave para acceder a la Raspberry.

Si tienes todavia la clave por defecto que crea el SO,  Tu Raspberry está en peligro y para ponerla a salvo, debemos cambiar la contraseña. eso lo haremas introduciendo en tu consola el siguiente comando:

```toml
sudo passwd
```
Pulsas enter y nos solicitará introducir la nueva contraseña para tu Raspberry dos veces. Con eso ya tenemos cambiada nuestra clave 

Para activar nuestro usuario root lo primero es asignarle una clave al usuario root esto es igual de sencillo que al usuario pi solo cambia algo en el comando

```toml
sudo passwd root
```

Y al igual que antes, pulsas enter y nos solicitará introducir la nueva contraseña dos veces.ya hemos asignado la clave. 
Al ejecutar este comando obtendras un mensaje y en alguan parte del mismo encontrarás una linea que será aprecida a esta:

Para habilitar el acceso a la raspberry por SSH como root editaremos el fichero de configuración `/etc/ssh/sshd_config` con el editor `nano`.


```toml
sudo nano /etc/ssh/sshd_config
```

Busca en el archivo el texto `#Authentication:` dentro de esta seecion encontrarás `PermitRootLogin`, en mi archivo es la linea 35 pero puede variar. D Debes sustituir lo que haya escrito despues de `PermitRootLogin` por yes, una vez editado debe quedar `PermitRootLogin yes`.

Cuando lo hayas modificado, pulsa `Ctrl + O` y despues Enter para guardar los cambios, y ahora debes cerrar el archivo pulsando `Ctrl + X`, una vez que reiniciemos el servicio el usuario root ya puede acceder via SSH a tu Raspberry usando la clave que le has asignado.

Escribe lo siguiente en tu consola, tanqui no apagas la Raspberry solo reinicias el servicio SSH

```toml
sudo service ssh restart
```
## Vayamos un poco mas allá.

Seguro que te preguntarás si has leido en el tutorial anterior la seccion [Vayamos un poco mas allá](/tutoriales/tutos-asignando-ip-estatica/#vayamos-un-poco-mas-all%C3%A1), si todo esto lo puede hacer un script, la respuesta es obvia, efectivamente **`si se puede`**, 

Aqui os dejo un ejemplo de como podeis cambiar la clave del usuario pi y activar el usuario root desde un archivo.

Puedes hacerlo siguiendo las instrucciones de [esta idea](/ideas/ideas-tu-primer-script-bash/) y escribir el archivo con el siguiente código:

```toml
# -------------------------------------------------------    
#                 Variables a utilizar                  *
# -------------------------------------------------------
#cambia true por false si no quieres que se ejecute

# cambiar clave pi
conf_pass=true

# Asignar clave y activar root
conf_pass_root=true

# Asignar una contraseña a las variable
new_password_user="tu clave nueva"
new password_root="tu clave nueva"


# -------------------------------------------------------    
# Cambiar clave del usuario Pi                          *
# -------------------------------------------------------

if [ "$conf_pass" = true ]; then
    clear
    
    echo "**************************************************************"
    echo "            Cambiando la contraseña del usuario Pi            "
    echo "**************************************************************"

    echo "pi:$new_password_user" | sudo chpasswd

    sleep 3

    echo "**************************************************************"
    echo "    El usuario pi ahora accede con la clave  $new_password_user    "
    echo "**************************************************************"

    else

    clear

    echo "**************************************************************"
    echo "   Nos saltamos la Configuración de la clave del usuario pi   "
    echo "**************************************************************"

    sleep 3
  
fi

# -------------------------------------------------------
# Autorizar acceso como root    REVISADO                *
# -------------------------------------------------------

if [ "$conf_pass_root" = true ]; then

    
    echo "**************************************************************"
    echo "           Asignando la contraseña del usuario root           "
    echo "**************************************************************"

    echo "root:$new_password_root" | sudo chpasswd

    sleep 3

    #modifica el archivo /etc/ssh/sshd_config
    #este comando busca cadenas a cambiar y si las encuentra lo hace
    sudo sed -i "s/#PermitRootLogin prohibit-password/PermitRootLogin yes/g" /etc/ssh/sshd_config
    sleep 3
    #reinicia servicio ssh
    sudo service ssh restart

    echo "**************************************************************"
    echo "               Ya puedes acceder como usuario root...         "
    echo "              Usando la contraseña $new_password_root             "
    echo "**************************************************************"
    
    sleep 3

    else

    echo "**************************************************************"
    echo "  Nos saltamos la Configuración de la clave del usuario root  "
    echo "**************************************************************"

    sleep 3
    
fi
```

## Y eso es todo.


Ya puedes acceder via SSH como root. Tambien puedes usarlo para subir archivos a tu servidor y modificar archivos por ftp o sftp con WinSCP o cualquier cliente de ftp. Otro tutorial pendiente.

{{< alert "circle-info" >}}
**Poco a poco** voy ampliando los contenidos de esta web con más tutoriales, ~~~~en breve podreis~~~~ ya podeis visitar tambien la seccion de [ideas](/ideas), con tutoriales cortos en los que mostraré como hacer cosas básicas
{{< /alert >}}

En la `siguiente parte` de esta serie os explicaré como cambiar Cambiar Locale y Timezone par adaptar el sistema a tu idioma y tu zona horaria. 
si no se alarga mucho cambiaremos el nombre de host.

🙋‍♀️ Recuerda, si necesitas algun consejo para empezar dejame un [mensaje de email](mailto:proyectopy@gmx.es) y trataré de ayudarte en la medida de mis posibilidades.

