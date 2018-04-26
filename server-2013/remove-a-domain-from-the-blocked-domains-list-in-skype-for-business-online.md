---
title: Quitar un dominio de la lista de dominios bloqueados
TOCTitle: Quitar un dominio de la lista de dominios bloqueados
ms:assetid: a11ea475-bb8b-44be-a5a5-4abb2fed42b8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362830(v=OCS.15)
ms:contentKeyID: 56271332
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Quitar un dominio de la lista de dominios bloqueados

 

_**Última modificación del tema:** 2015-06-22_

Se deben seguir dos pasos para quitar un dominio de la lista de dominios bloqueados. Primero debe usar el cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) para crear un objeto de dominio para el dominio que quitará:

    $x = New-CsEdgeDomainPattern "fabrikam.com"

Una vez que lo haga, use la siguiente sintaxis para quitar el dominio (en este ejemplo, el que está almacenado en la variable $x) de la lista de dominios bloqueados:

    Set-CsTenantFederationConfiguration -BlockedDomains @{Remove=$x}

Para quitar todos los dominios de la lista de dominios bloqueados, establezca el valor de la propiedad BlockedDomains en null ($Null):

    Set-CsTenantFederationConfiguration -BlockedDomains $Null

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

