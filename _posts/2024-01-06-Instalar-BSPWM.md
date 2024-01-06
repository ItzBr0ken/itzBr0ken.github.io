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

Una vez dentro del sistema de BSPWM podemos ajustar la resolucion a la pantalla del escritorio remoto utilizando XRANDR y ARANDR

