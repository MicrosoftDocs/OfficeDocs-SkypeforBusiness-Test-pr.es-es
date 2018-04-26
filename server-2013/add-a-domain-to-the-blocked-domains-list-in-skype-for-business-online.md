---
title: 'Lync Online: Agregar un dominio a la lista de dominios bloqueados'
TOCTitle: Agregar un dominio a la lista de dominios bloqueados
ms:assetid: ea6ebeea-3031-4c42-9a2c-88eaab790636
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362853(v=OCS.15)
ms:contentKeyID: 56271370
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Agregar un dominio a la lista de dominios bloqueados en Lync Online

 

_**Última modificación del tema:** 2015-06-22_

Para agregar un dominio a la lista de dominios bloqueados, use una sintaxis similar a la siguiente:

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -BlockedDomains @{Add=$x}

Como puede ver, este comando requiere dos pasos. En primer lugar, utilice el [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) para crear un objeto de dominio que representa el dominio se debe agregar a la lista de bloqueados. A continuación, utilice el cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) y el método Add para agregar ese dominio (en este ejemplo, el dominio almacenado en la variable $x) a la lista.

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

