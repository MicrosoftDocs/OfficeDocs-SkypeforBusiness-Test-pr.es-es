---
title: Se ha excedido el número máximo de shells simultáneos para este inquilino
TOCTitle: Se ha excedido el número máximo de shells simultáneos para este inquilino
ms:assetid: a4c91ffa-fdcc-414c-b941-a0d36c906825
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362832(v=OCS.15)
ms:contentKeyID: 56271341
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Se ha excedido el número máximo de shells simultáneos para este inquilino

 

_**Última modificación del tema:** 2015-06-22_

Mientras que los administradores pueden tener hasta tres conexiones simultáneas a un inquilino de Skype Empresarial Online, los inquilinos no pueden tener más de nueve. Por ejemplo, suponga que tres administradores tienen tres sesiones abiertas cada uno. Si un cuarto administrador intenta establecer una conexión (lo que da como resultado un total de diez conexiones simultáneas), se producirá un error y aparecerá el siguiente mensaje:

    New-PSSession : [admin.vdomain.com] Error al conectarse al servidor remoto admin.vdomain.com. Mensaje de error: El servicio WS-Management no puede procesar la solicitud. Se ha superado el número máximo de shells simultáneos de este inquilino. Cierre los shells existentes o aumente la cuota del inquilino. Para obtener más información, vea el tema de ayuda about_Remote_Troubleshooting.

La única manera de resolver este problema es cerrar una o varias de las conexiones anteriores. Cuando ya no use una sesión de Skype Empresarial Online, le recomendamos usar el cmdlet **Remove-PSSession** para cerrarla. De este modo, evitará que se produzca este problema.

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

