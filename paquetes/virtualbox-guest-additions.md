---
description: >-
  VirtualBox Guest Additions consiste en controladores de dispositivos que
  permiten una mejor resolución de pantalla e integración del mouse.
---

# Virtualbox guest additions

VirtualBox Guest Additions consiste en controladores de dispositivos que permiten una mejor resolución de pantalla e integración del mouse. Optimizarán tu sistema operativo en cuanto a rendimiento y usabilidad. En este tutorial, instalaremos Virtualbox Guest Additions en Ubuntu 20.04 LTS Focal Fossa Linux.

La forma más fácil de instalar las adiciones de invitados de Virtualbox en Ubuntu 20.04 LTS Focal Fossa es instalar los siguientes paquetes desde el repositorio estándar de Ubuntu:

```
sudo add-apt-repository multiverse
sudo apt install virtualbox-guest-dkms virtualbox-guest-x11
```

Una vez finalizada la instalación, procede a reiniciar el servidor.

Confirme las adiciones de invitados de Virtualbox:

```
lsmod  | grep vbox
vboxsf                 81920  0
vboxguest             344064  6 vboxsf
```
