---
title: Anular la asignación de una directiva por usuario asignada anteriormente a un usuario
TOCTitle: Anular la asignación de una directiva por usuario asignada anteriormente a un usuario
ms:assetid: bdba1d22-28e4-4203-a109-a3fb408783d3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362840(v=OCS.15)
ms:contentKeyID: 56271350
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Anular la asignación de una directiva por usuario asignada anteriormente a un usuario

 

_**Última modificación del tema:** 2015-06-22_

Si quiere cancelar la asignación de una directiva por usuario realizada anteriormente a un usuario, vuelva a ejecutar el cmdlet **Grant-Cs** correspondiente (por ejemplo, el cmdlet [Grant-CsVoicePolicy](grant-csvoicepolicy.md) para cancelar la asignación de una directiva de voz) y establezca el parámetro PolicyName en null ($Null):

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

Para cancelar la asignación de directivas de voz de todos los usuarios, use este comando:

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName $Null

Cuando se cancela una asignación de un usuario, este se administra con la directiva global.

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

