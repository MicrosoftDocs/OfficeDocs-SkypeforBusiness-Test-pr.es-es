---
title: Se ha excedido el número máximo de shells simultáneos para este usuario
TOCTitle: Se ha excedido el número máximo de shells simultáneos para este usuario
ms:assetid: b309efe8-a214-41ea-a345-93e6a36e0cb1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362837(v=OCS.15)
ms:contentKeyID: 56271348
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Se ha excedido el número máximo de shells simultáneos para este usuario

 

_**Última modificación del tema:** 2015-06-22_

Los administradores pueden tener hasta tres conexiones remotas simultáneas a Skype Empresarial Online. Si tiene tres conexiones de Windows PowerShell remotas en funcionamiento e intenta establecer una cuarta conexión simultánea, se producirá un error y recibirá el siguiente mensaje:

    New-PSSession : [admin.vdomain.com] Error al conectarse al servidor remoto admin.vdomain.com. Mensaje de error: El servicio WS-Management no puede procesar la solicitud. Se ha superado el número máximo de shells simultáneos de este usuario. Cierre los shells existentes o aumente la cuota del usuario.Para obtener más información, vea el tema de ayuda about_Remote_Troubleshooting

La única manera de resolver este problema es cerrar una o varias de las conexiones anteriores. Cuando ya no use una sesión de Skype Empresarial Online, le recomendamos usar el cmdlet **Remove-PSSession** para cerrarla. De este modo, evitará que se produzca este problema.

## Vea también

#### Conceptos

[Diagnosticar y resolver los problemas de conexión con Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

