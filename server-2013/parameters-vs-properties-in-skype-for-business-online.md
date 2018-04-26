---
title: Parámetros y propiedades
TOCTitle: Parámetros y propiedades
ms:assetid: 65348f95-f4d4-40cd-8869-f9d72643792d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362796(v=OCS.15)
ms:contentKeyID: 56271303
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Parámetros y propiedades

 

_**Última modificación del tema:** 2015-06-22_

Al leer los temas de ayuda de los cmdlets de Skype Empresarial Online, algunas veces verá que los términos *parámetro* y *propiedad* se usan indistintamente. No se deje confundir por la terminología: aunque técnicamente ambos son diferentes, en Skype Empresarial Online estos términos se refieren básicamente a lo mismo.

Desde el punto de vista técnico, los parámetros se usan al ejecutar un cmdlet. Por ejemplo, en el siguiente comando de Windows PowerShell, EnableMicrosoftPushNotificationService y EnableApplePushNotificationService son parámetros del cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md):

    Set-CsPushNotificationConfiguration -EnableMicrosoftPushNotificationService -EnableApplePushNotificationService $True

Una propiedad es un atributo de un objeto de Skype Empresarial Online (por ejemplo, una colección de opciones de configuración de notificaciones de inserción). Supongamos que ejecuta este comando:

    Set-CsPushNotificationConfiguration

Al hacerlo, recibirá una colección de propiedades y sus valores asociados, que incluyen los elementos siguientes:

    EnableMicrosoftPushNotificationService : True
    EnableApplePushNotificationService     : True

Como puede ver, las propiedades y los parámetros comparten el mismo nombre: usamos el parámetro EnableMicrosoftPushNotificationService para configurar el valor de la propiedad EnableMicrosoftPushNotificationService.

## Vea también

#### Conceptos

[Introducción a Windows PowerShell y Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

