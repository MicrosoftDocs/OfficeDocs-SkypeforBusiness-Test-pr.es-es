---
title: El usuario no tiene permiso para administrar este inquilino
TOCTitle: El usuario no tiene permiso para administrar este inquilino
ms:assetid: 714ccf81-9451-4585-b62d-979f2a606315
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362812(v=OCS.15)
ms:contentKeyID: 56271322
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# El usuario no tiene permiso para administrar este inquilino

 

_**Última modificación del tema:** 2015-06-22_

No puede establecer una conexión remota de Windows PowerShell con Skype Empresarial Online a menos que sea miembro del grupo Administradores de inquilinos. Si no lo es, el intento de conexión fallará y verá el mensaje de error siguiente:

    New-PSSession : [admin.vdomain.com] Error al procesar datos del servidor remoto admin.vdomain.com. Mensaje de error: El usuario "user@foo.com" no tiene permiso para administrar este inquilino. Los permisos se pueden otorgar al asignar al usuario a la función RBAC adecuada.Para obtener más información, vea el tema de ayuda about_Remote_Troubleshooting.

Si cree que es o debería ser miembro del grupo Administradores de inquilinos, póngase en contacto con el soporte técnico de Office 365.

## Vea también

#### Conceptos

[Diagnosticar y resolver los problemas de conexión con Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

