---
title: Introducción a Windows PowerShell y Lync Online
TOCTitle: Introducción a Windows PowerShell y Lync Online
ms:assetid: 4b4cf534-c950-4d6c-abd9-d3d0e6f53bb7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362785(v=OCS.15)
ms:contentKeyID: 56271282
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Introducción a Windows PowerShell y Lync Online

 

_**Última modificación del tema:** 2015-06-22_

Windows PowerShell es un shell de comandos y un lenguaje de scripting que se puede usar para administrar Skype Empresarial Online. En lugar de usar el centro de administración gráfico de Skype Empresarial Online para administrar Skype Empresarial Online, puede administrar el producto usando comandos de la línea de comandos parecidos a este:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Además de usar comandos simples como el del ejemplo anterior (que devuelve información sobre un usuario cuyo UPN es kenmyer@litwareinc.com), los usuarios con más experiencia en Windows PowerShell también pueden organizar estos comandos en scripts, que se pueden usar para automatizar procesos y/o llevar a cabo tareas repetitivas.

Como norma general, cualquier tarea que se pueda hacer usando el centro de administración de Skype Empresarial Online también se podrá hacer usando Windows PowerShell. Por ejemplo, puede usar el centro de administración para administrar las notificaciones de teléfono móvil, también denominadas *notificaciones de inserción*. Las notificaciones de inserción permiten enviar notificaciones sobre eventos (como pueden ser mensajes instantáneos o correos de voz nuevos) a dispositivos móviles, como iPhone y Windows Phone. Estas notificaciones se reciben en el dispositivo móvil aunque la aplicación de Lync de los dispositivos se esté ejecutando en segundo plano.

¿Cómo se administran las notificaciones de inserción? Una forma de hacerlo es usar el centro de administración de Skype Empresarial Online, donde puede habilitar o deshabilitar las notificaciones de inserción seleccionando la opción correspondiente en la pestaña **organización**:

![LyncOnlinePowerShell\_Push\_Notifications](images/Dn362807.0a6ec1f5-1999-427f-880b-0587c98d7670(OCS.15).png "LyncOnlinePowerShell_Push_Notifications")

También puede habilitar o deshabilitar las notificaciones de inserción usando una sesión remota de Windows PowerShell y el cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md). Por ejemplo, este comando deshabilita las notificaciones de inserción para los dispositivos iPhone y Windows Phone:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Como puede ver, los parámetros (es decir, EnableApplePushNotificationService y EnableMicrosoftPushNotificationService), usados con el cmdlet **Set-CsPushNotificationConfiguration**, se corresponden con las opciones disponibles en el centro de administración de Skype Empresarial Online:

![Asociación mostrada entre las opciones de Lync y el cmdlet de PS](images/Dn362785.f20086fd-3b51-4bbf-8d81-e643d9bf3a2e(OCS.15).png "Asociación mostrada entre las opciones de Lync y el cmdlet de PS")

En resumen, para administrar las notificaciones de inserción, podemos usar, bien el centro de administración, bien un cmdlet de Windows PowerShell y los parámetros adecuados. Ambos métodos son válidos y funcionan igual de bien.


> [!NOTE]
> Para consultar las definiciones de términos concretos de Windows PowerShell, como <EM>cmdlet</EM>, <EM>parámetro</EM>, <EM>valor de parámetro</EM> y <EM>argumento</EM>, vea <A href="windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md">Cmdlets, parámetros y valores de parámetro de Windows PowerShell</A>.



Esto suscita una cuestión obvia: si el centro de administración de Skype Empresarial Online y Windows PowerShell ofrecen exactamente las mismas funciones, ¿por qué elegir usar una opción en lugar de la otra? ¿Y por qué elegir escribir comandos en Windows PowerShell en vez de simplemente seleccionar o desactivar casillas en el centro de administración?

En un caso simple como el del ejemplo anterior, decidir qué método queremos usar es una preferencia personal: algunas personas prefieren usar una interfaz de usuario gráfica, mientras que otras prefieren una herramienta de línea de comandos, como Windows PowerShell. Sin embargo, en algunos casos, Windows PowerShell es el medio más eficaz para realizar una tarea de administración o el único medio para hacerla. Por ejemplo, el centro de administración de Skype Empresarial Online le permite personalizar invitaciones a reuniones:

![Configuración de invitación a reunión en el centro de administración de Lync](images/Dn362785.3fb00c33-0bd4-46dd-beb1-8f71e24cf630(OCS.15).png "Configuración de invitación a reunión en el centro de administración de Lync")

Estas mismas personalizaciones se pueden hacer con el cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md). Sin embargo, el cmdlet **Set-CsMeetingConfiguration** incluye, además, opciones que no están disponibles en el centro de administración de Skype Empresarial Online. Por ejemplo, si alguien de la organización se une a una reunión, se le configura automáticamente como moderador de la reunión de manera predeterminada. Esta configuración no se puede cambiar desde el centro de administración de Skype Empresarial Online: solo se puede cambiar usando Windows PowerShell y el cmdlet **Set-CsMeetingConfiguration**. Concretamente, este comando establece la propiedad DesignateAsPresenter en None, que significa que solo el organizador de la reunión se puede configurar como moderador al unirse a la reunión:

    Set-CsMeetingConfiguration -DesignateAsPresenter "Everyone"

Si quiere detalles sobre el uso de Windows PowerShell, vea los temas siguientes:

  - [Cmdlets, parámetros y valores de parámetro de Windows PowerShell](windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md)

  - [Trabajar con parámetros](working-with-parameters-in-skype-for-business-online.md)

  - [Parámetros opcionales y obligatorios](mandatory-and-optional-parameters-in-skype-for-business-online.md)

  - [Parámetros y propiedades](parameters-vs-properties-in-skype-for-business-online.md)

  - [Combinar cmdlets de Lync Online y Windows PowerShell](combining-skype-for-business-online-cmdlets-with-other-windows-powershell-cmdlets-in.md)

  - [Más ayuda sobre el uso de Windows PowerShell](more-help-for-using-windows-powershell-in-skype-for-business-online.md)

