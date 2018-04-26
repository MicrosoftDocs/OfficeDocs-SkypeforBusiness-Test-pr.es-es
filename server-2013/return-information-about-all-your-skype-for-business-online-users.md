---
title: Obtener información sobre todos los usuarios de Lync Online
TOCTitle: Obtener información sobre todos los usuarios de Lync Online
ms:assetid: 0b59fadf-67e6-48ea-86f1-2efef500ebdf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362769(v=OCS.15)
ms:contentKeyID: 56271263
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener información sobre todos los usuarios de Lync Online

 

_**Última modificación del tema:** 2015-06-22_

Para devolver información sobre todos los usuarios que se han habilitado para Skype Empresarial Online, llame al cmdlet [Get-CsOnlineUser](get-csonlineuser.md) sin ningún parámetro adicional:

    Get-CsOnlineUser

Para devolver información sobre un solo usuario seleccionado al azar (por ejemplo, para usar esta cuenta para hacer pruebas), llame al cmdlet **Get-CsOnlineUser** y establezca el parámetro ResultSize en 1:

    Get-CsOnlineUser -ResultSize 1

Esto hace que el cmdlet **Get-CsOnlineUser** devuelva información sobre un solo usuario independientemente del número de usuarios que haya en la organización. Para devolver información sobre cinco usuarios, establezca el valor del parámetro ResultSize en 5:

    Get-CsOnlineUser -ResultSize 5

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

