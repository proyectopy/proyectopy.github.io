---
title: "Ideas | Problemas al instalar Apache"
date: 2022-12-06T11:03:56+01:00
draft: true
showTableOfContents : false
description: "Soluciona los problemas al intalar apache."
slug: "ideas-problemas-al-instalar-Apache"
tags: ["problemas", "instalaciones", "servidores", "apache", "bash"]

---

Algunas veces al instalar/desinstalar algun servicio, surgen problemas y entre ellos al desinstalar apache e intentar reinstalarlo, es algo muy comun.


Puedes ver todas las ideas que se me van ocurriendo [aquí](/ideas).

## Problemas conocidos reinstalando Apache.

Solucion al problema.....

```toml
sudo a2dissite 000-default

sudo service apache2 reload

sudo apt-get purge apache2 apache2-utils apache2.2-bin apache2-common

sudo apt-get --purge remove -y apache2

sudo apt-get autoremove --purge -y

sudo apt-get purge apache2-data

sudo cp -r  /var/www /var/www_backup

sudo rm -r /var/www
```

install

```toml
sudo apt-get install -y apache2
```
si sigue fallando 

```toml
sudo apt install --reinstall apache2-bin   
sudo service apache2 start  
```