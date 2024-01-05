---
# the default layout is 'page'
icon: fas fa-cog
title: Instalar Proxmox
author: Uri
date: 2024-01-01 14:10:00 +0100
categories: [Informática, Instalar Proxmox]
tags: [Informática, Proxmox]
render_with_liquid: false
order: 5
---

# Introducción

Proxmox VE es una plataforma de servidor de código abierto para virtualización empresarial. Como distribución de Linux basada en Debian, Proxmox utiliza un kernel de Ubuntu modificado para ejecutar múltiples máquinas virtuales y contenedores en un solo servidor. Puede implementar y administrar entornos virtualizados a través de una consola web o una línea de comandos, lo que garantiza una accesibilidad sencilla y rápida.

Continúe leyendo para descubrir cómo instalar y configurar Proxmox.

# Requisitos previos

* Un servidor físico o dedicado.
* CPU de 64 bits .
* Al menos 1 GB de RAM (y se necesita RAM adicional para los invitados).
* Una memoria USB de al menos 1 GB.

# Instalar el entorno virtual Proxmox

Siga los pasos que se enumeran a continuación para instalar Proxmox VE en un servidor físico o dedicado.

## Paso 1: descargue la imagen ISO de Proxmox

El primer paso es descargar la imagen ISO de Proxmox VE.

* Navegue a la página oficial de Descargas de Proxmox y seleccione Entorno virtual de Proxmox .

![Desktop View](/assets/img/proxmox/prox1.png){: .normal }

* Esto lo llevará al Archivo del entorno virtual de Proxmox que almacena imágenes ISO y documentación oficial. Seleccione Imágenes ISO para continuar.

![Desktop View](/assets/img/proxmox/prox2.png){: .normal }

* En el momento de escribir este artículo, la última versión del instalador Proxmox VE ISO es 7.1. Si hay una versión más nueva disponible, aparece en la parte superior. Haga clic en Descargar y guarde el archivo.

![Desktop View](/assets/img/proxmox/prox3.png){: .normal }

## Paso 2: preparar el medio de instalación

Copie la imagen ISO de Proxmox en un CD/DVD o una unidad flash USB. Aunque ambas opciones son posibles, se supone que la mayoría de los sistemas no tendrán una unidad óptica.

Conecte la unidad USB y copie la imagen ISO en la memoria USB usando la línea de comando o una utilidad de formateo USB (como Etcher o Rufus).

## Paso 3: inicie el instalador de Proxmox

* Vaya al servidor (máquina) donde desea instalar Proxmox y conecte el dispositivo USB.
* Mientras el servidor se está iniciando, acceda al menú de inicio presionando las teclas del teclado requeridas. Lo más común es que sean Esc , F2 , F10 , F11 o F12 .
* Seleccione el medio de instalación con la imagen ISO de Proxmox y arranque desde allí.
* A continuación, aparece el menú de Proxmox VE. Seleccione Instalar Proxmox VE para iniciar la instalación estándar.
* Lea y acepte el EULA para continuar.
* Elija el disco duro de destino donde desea instalar Proxmox. Haga clic en Opciones para especificar parámetros adicionales, como el sistema de archivos. De forma predeterminada, está configurado en ext4.

* Luego, configure la ubicación, la zona horaria y la distribución del teclado. El instalador detecta automáticamente la mayoría de estas configuraciones.
* Cree una contraseña segura para sus credenciales de administrador, vuelva a escribir la contraseña para confirmarla y escriba una dirección de correo electrónico para recibir notificaciones del administrador del sistema.
* El último paso para instalar Proxmox es establecer la configuración de red. Seleccione la interfaz de administración, un nombre de host para el servidor, una dirección IP disponible, la puerta de enlace predeterminada y un servidor DNS . Durante el proceso de instalación, utilice una dirección IPv4 o IPv6 . Para usar ambos, modifique la configuración después de la instalación.
* El instalador resume las opciones seleccionadas. Después de confirmar que todo está en orden, presione Instalar.
* Una vez completada la instalación, retire la unidad USB y reinicie el sistema.

## Paso 4: Ejecute Proxmox

* Una vez que se completa la instalación y el sistema se reinicia, se carga el menú de Proxmox GRUB. Seleccione Entorno Virtual Proxmox GNU/Linux y presione Enter .
* A continuación, aparece el mensaje de bienvenida de Proxmox VE. Incluye una dirección IP que carga Proxmox. Navegue hasta esa dirección IP en un navegador web de su elección.
* Después de navegar a la dirección IP requerida, lo más probable es que vea un mensaje de advertencia que indica que la página no es segura porque Proxmox VE utiliza certificados SSL autofirmados . Seleccione para proceder a la interfaz de administración web de Proxmox.
* Para acceder a la interfaz, inicie sesión como root y proporcione la contraseña establecida al instalar Proxmox.
* Aparece un cuadro de diálogo que indica que no hay una suscripción válida para el servidor. Proxmox ofrece un servicio complementario al que puedes suscribirte, que es opcional. Para ignorar el mensaje, haga clic en Aceptar .

## Paso 5: crear una máquina virtual

Ahora que inició sesión en la consola web de Proxmox, cree una máquina virtual.

* Antes de seguir los pasos para crear una máquina virtual, asegúrese de tener imágenes ISO para los medios de instalación. Vaya al árbol de recursos en el lado izquierdo de su GUI.
Seleccione el servidor que está ejecutando y haga clic en local (pve1) . Seleccione Imágenes ISO en el menú y elija entre cargar una imagen o descargarla desde una URL.
* Una vez que haya agregado una imagen ISO, continúe con la puesta en marcha de una máquina virtual. Haga clic en el botón Crear VM ubicado en el lado derecho del encabezado en la GUI.
* Proporcione información general sobre la VM:
1. Comience seleccionando el Nodo . Si está comenzando y aún no tiene nodos, Proxmox selecciona automáticamente el nodo 1 ( pve1 ).
2. Proporcione una identificación de máquina virtual . Cada recurso debe tener una identificación única.
3. Finalmente, cree un nombre para la VM. Utilice un nombre fácilmente identificable.
* A continuación, cambie a la pestaña SO y seleccione la imagen ISO que desea para su VM. Defina el tipo de sistema operativo y la versión del kernel . Haga clic en Siguiente para continuar.
* Modifique las opciones del sistema (como la tarjeta gráfica y el controlador SCSI ) o deje la configuración predeterminada.
* Luego, configure las opciones de disco duro que desee que tenga la máquina virtual. Generalmente, puedes dejar todas las configuraciones predeterminadas. Sin embargo, si el servidor físico utiliza un SSD, habilite la opción Descartar .
* La cantidad de núcleos que tiene el servidor físico determina cuántos núcleos puede proporcionar a la VM. La cantidad de núcleos asignados también depende de la carga de trabajo prevista.
* A continuación, elija cuánta memoria (MiB) desea asignar a la VM.
* Pase a la pestaña Red . Se recomienda separar la interfaz de administración y la red VM. Por ahora, deje la configuración predeterminada.
* Después de hacer clic en  Siguiente , Proxmox carga la pestaña Confirmar que resume las opciones de VM seleccionadas. Para iniciar la VM inmediatamente, marque la casilla debajo de la información que aparece o inicie la VM manualmente más tarde. Haga clic en Finalizar para crear la VM.
* Vea la VM recién creada en el árbol de recursos en el lado izquierdo de la pantalla. Haga clic en la VM para ver sus especificaciones y opciones.








