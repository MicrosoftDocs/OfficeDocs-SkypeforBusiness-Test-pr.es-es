---
title: Obtener una lista filtrada de usuarios
TOCTitle: Obtener una lista filtrada de usuarios
ms:assetid: f2c4d13b-8601-4192-8b94-e9a57969da11
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362858(v=OCS.15)
ms:contentKeyID: 56271372
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener una lista filtrada de usuarios

 

_**Última modificación del tema:** 2015-06-22_

Use el cmdlet [Get-CsOnlineUser](get-csonlineuser.md) y los parámetros LdapFilter o Filter para obtener información rápidamente sobre un conjunto de usuarios de destino. Por ejemplo, este comando devuelve todos los usuarios que trabajan en el departamento financiero:

    Get-CsOnlineUser -LdapFilter "department=Finance"

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

