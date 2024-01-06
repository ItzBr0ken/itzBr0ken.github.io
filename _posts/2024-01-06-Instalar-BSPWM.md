---
# the default layout is 'page'
icon: fas fa-cog
title: Instalar BSPWM en Kali linux
author: Uri
date: 2024-01-06 12:10:00 +0100
categories: [Informática, Kali Linux - BSPWM]
tags: [Informática, BSPWM, Instalar, Kali, Linux]
render_with_liquid: false
mermaid: true
comments: true
image: /assets/img/bspwm.jpg
order: 5
---

## Como instalar BSPWM en Kali linux

Para instalar BSPWM en Kali linux utilizar el siguiente script

```
git clone https://github.com/xJackSx/BSPWMkali.git
cd BSPWMkali
chmod +x install.sh
./install.sh
```

## Acceder remotamente a BSPWM

En el caso de que el ordenador sea un ordenador remoto vamos a habilitar ciertas funciones para poder acceder remotamente

```
echo bspwm > ~/.xsessions 
apt-get install xrdp -y 
systemctl start xrdp 
systemctl enable xrdp 
apt-get install ufw 
ufw allow ssh
ufw allow 3389 
ufw start 
```

## Ajustar el escritorio para utilizar remotamente a BSPWM

Una vez dentro del sistema de BSPWM podemos ajustar la resolución a la pantalla del escritorio remoto utilizando `xrandr` y `arandr`. Primero, instalaremos los paquetes ejecutaremos el comando ARANDR y guardaremos la configuración

```
apt-get install arandr
arandr
```

Una vez guardado el archivo de la resolución deseada se guardara en formato de script ejecutable (.sh). Seguidamente, nos dirigiremos a la siguiente carpeta

```
cd /home/usuario/.config/bspwm
```
Donde, en la palabra `usuario` debemos sustituirla por nuestro usuario linux. Después, modificar el archivo bspwmrc

```
nano bspwmrc
```
Una vez dentro, buscaremos el apartado que aparece como `#RESOLUCION ARANDR`. Introduciremos la dirección del archivo en este punto del documento

```
/home/usuario/archivo.sh
```
Recuerde sustituir la palabra `usuario` por la del usuario de linux y la palabra `archivo` por la del nombre del archivo guardado previamente con la funcion `arandr`.

> Ten en cuenta que la dirección del archivo (`path`) puede ser diferente de la descrita anteriormente.
{: .prompt-warning }

