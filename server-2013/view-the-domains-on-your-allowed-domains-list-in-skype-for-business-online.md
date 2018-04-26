---
title: Ver los dominios de la lista de dominios permitidos
TOCTitle: Ver los dominios de la lista de dominios permitidos
ms:assetid: 13bceaba-5c4f-431f-864f-9e374cafa986
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362772(v=OCS.15)
ms:contentKeyID: 56271270
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ver los dominios de la lista de dominios permitidos

 

_**Última modificación del tema:** 2015-06-22_

Para ver todos los dominios que tiene en la lista de dominios permitidos, use [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) y la sintaxis siguiente:

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty AllowedDomains | Select-Object AllowedDomain

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

