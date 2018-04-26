---
title: Se ha deshabilitado la capacidad de conectar con el inquilino
TOCTitle: Se ha deshabilitado la capacidad de conectar con el inquilino
ms:assetid: 7365d31b-173e-4339-b0a3-98ab73a9558f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362820(v=OCS.15)
ms:contentKeyID: 56271319
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Se ha deshabilitado la capacidad de conectar con el inquilino

 

_**Última modificación del tema:** 2015-06-22_

Si quiere usar Windows PowerShell para administrar Skype Empresarial Online, la propiedad EnableRemotePowerShellAccess de la directiva de Windows PowerShell de su inquilino se debe establecer en True. Si no se hace, el intento de conexión fallará y verá el mensaje de error siguiente:

    New-PSSession : [admin.vdomain.com] Error al procesar datos del servidor remoto admin.vdomain.com. Mensaje de error: Se ha deshabilitado la opción de conectarse a este inquilino mediante la sesión remota de PowerShell. Póngase en contacto con el servicio de ayuda de Lync para comprobar la directiva de inquilino de PowerShell para este inquilino.Para obtener más información, vea el tema de ayuda about_Remote_Troubleshooting.

Si ve este mensaje de error, póngase en contacto con el soporte técnico de Office 365 y pida que le habiliten el acceso remoto a Windows PowerShell.

## Vea también

#### Conceptos

[Diagnosticar y resolver los problemas de conexión con Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

