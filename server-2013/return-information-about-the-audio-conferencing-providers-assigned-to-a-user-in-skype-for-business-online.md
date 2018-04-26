---
title: Obtener información sobre los proveedores de servicios de audioconferencia asignados a un usuario
TOCTitle: Obtener información sobre los proveedores de servicios de audioconferencia asignados a un usuario
ms:assetid: 7fae822f-9f6c-4381-95c5-879661027925
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362814(v=OCS.15)
ms:contentKeyID: 56271295
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener información sobre los proveedores de servicios de audioconferencia asignados a un usuario

 

_**Última modificación del tema:** 2015-06-22_

Para devolver información sobre los proveedores de audioconferencia que se han asignado a un usuario, use el cmdlet [Get-CsUserAcp](get-csuseracp.md) y esta sintaxis:

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

