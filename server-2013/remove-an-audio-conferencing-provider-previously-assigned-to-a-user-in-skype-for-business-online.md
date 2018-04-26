---
title: Quitar un proveedor de servicios de audioconferencia asignado anteriormente a un usuario
TOCTitle: Quitar un proveedor de servicios de audioconferencia asignado anteriormente a un usuario
ms:assetid: 85d59e6c-d646-4908-9767-adb48763f6de
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362808(v=OCS.15)
ms:contentKeyID: 56271297
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Quitar un proveedor de servicios de audioconferencia asignado anteriormente a un usuario

 

_**Última modificación del tema:** 2015-06-22_

Para quitar todos los proveedores de audioconferencia asignados a un usuario, ejecute el cmdlet [Remove-CsUserAcp](remove-csuseracp.md) sin ningún parámetro (fuera del parámetro Identity, que indica el usuario en cuestión):

    Remove-CsUserAcp -Identity "Ken Myer"

Si a un usuario se le han asignado varios proveedores de audioconferencia, puede eliminar uno solo incluyendo el parámetro Name seguido del nombre del proveedor que quiere quitar:

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Contoso ACP"

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

