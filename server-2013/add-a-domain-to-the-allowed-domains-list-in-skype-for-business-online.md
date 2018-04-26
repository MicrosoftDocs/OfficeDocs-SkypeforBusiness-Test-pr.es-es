---
title: 'Lync Online: Agregar un dominio a la lista de dominios admitidos'
TOCTitle: Agregar un dominio a la lista de dominios admitidos
ms:assetid: 7b7f76c8-3047-40be-a938-8ac2868a6bc8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362818(v=OCS.15)
ms:contentKeyID: 56271300
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Agregar un dominio a la lista de dominios admitidos en Lync Online

 

_**Última modificación del tema:** 2015-06-22_

La adición de un dominio primero a la lista de dominios permitidos es un proceso de tres pasos. En primer lugar, utilice el cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) para crear un objeto de dominio para el dominio que se agregará:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

A contiuación, use el cmdlet [New-CsEdgeAllowList](new-csedgeallowlist.md) para crear una nueva lista de permitidos que incluya el objeto de dominio:

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x

Por último, use el cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) para escribir la nueva lista de permitidos en Skype Empresarial Online:

    Set-CsTenantFederationConfiguration -AllowedDomains $newAllowList

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

