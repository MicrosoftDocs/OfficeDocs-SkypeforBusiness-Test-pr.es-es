---
title: Habilitar o deshabilitar las notificaciones de inserción en dispositivos iPhone y Windows Phone
TOCTitle: Habilitar o deshabilitar las notificaciones de inserción en dispositivos iPhone y Windows Phone
ms:assetid: 64482dcb-6354-4fb5-a2e4-1564b3d0e047
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362792(v=OCS.15)
ms:contentKeyID: 56271308
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Habilitar o deshabilitar las notificaciones de inserción en dispositivos iPhone y Windows Phone

 

_**Última modificación del tema:** 2015-06-22_

Para deshabilitar las notificaciones de inserción y evitar que se envíen a dispositivos iPhone o Windows Phone, use el cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) y establezca los valores de las propiedades EnableApplePushNotificationService y EnableMicrosoftPushNotificationService en False ($False):

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Los dispositivos iPhone y Windows Phone se pueden configurar por separado. Este comando, por ejemplo, deshabilita las notificaciones de inserción en los iPhone, pero las habilita en los Windows Phone:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $True

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

