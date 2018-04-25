---
title: Asignar una directiva por usuario a un usuario
TOCTitle: Asignar una directiva por usuario a un usuario
ms:assetid: 37e07da7-6391-4d6d-a428-c70272897039
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362779(v=OCS.15)
ms:contentKeyID: 56271276
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Asignar una directiva por usuario a un usuario

 

_**Última modificación del tema:** 2015-06-22_

Para asignar una directiva por usuario a un usuario, primero hay que seleccionar el cmdlet **Grant-Cs** adecuado. (Por ejemplo, para asignar una directiva por usuario de voz, sería [Grant-CsVoicePolicy](grant-csvoicepolicy.md)). Ejecute el cmdlet asegurándose de especificar la identidad del usuario al que se le debe asignar la directiva y el nombre de la directiva que quiere asignar:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

Si quiere asignar la misma directiva a todos los usuarios, use esta sintaxis:

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName "RedmondVoicePolicy"

Recuerde que, debido a las diferencias en los acuerdos de licencia y en las restricciones de país o región, puede que algunas directivas de conferencia, de acceso externo o de movilidad no se puedan asignar a un usuario concreto. Para ver las directivas por usuario que sí se pueden asignar a un usuario determinado (por ejemplo, kenmyer@litwareinc.com), use uno de los comandos siguientes (y el parámetro ApplicableTo) según corresponda:

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

La sintaxis anterior solo devuelve las directivas por usuario que se pueden asignar a Ken Myer.

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

