---
title: Ver los dominios de la lista de dominios bloqueados
TOCTitle: Ver los dominios de la lista de dominios bloqueados
ms:assetid: 67c65dbf-1a68-4c77-aabd-bed5001b4267
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362797(v=OCS.15)
ms:contentKeyID: 56271307
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ver los dominios de la lista de dominios bloqueados

 

_**Última modificación del tema:** 2015-06-22_

Para ver todos los dominios que tiene en la lista de dominios bloqueados, llame al cmdlet [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) y canalice los datos devueltos hacia el cmdlet **Select-Object**:

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty BlockedDomains

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

