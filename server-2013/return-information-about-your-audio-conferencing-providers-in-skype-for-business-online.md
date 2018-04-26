---
title: Obtener información sobre los proveedores de servicios de audioconferencia
TOCTitle: Obtener información sobre los proveedores de servicios de audioconferencia
ms:assetid: df9c8fc0-8bb6-4416-a5cc-aa9b1601a688
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362848(v=OCS.15)
ms:contentKeyID: 56271357
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener información sobre los proveedores de servicios de audioconferencia

 

_**Última modificación del tema:** 2015-06-22_

Para recibir información de los proveedores de servicios de audioconferencia que se encuentran asignados a un usuario, use el cmdlet [Get-CsUserAcp](get-csuseracp.md) y la siguiente sintaxis:

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

