---
title: Quitar un dominio de la lista de dominios permitidos
TOCTitle: Quitar un dominio de la lista de dominios permitidos
ms:assetid: 04948582-363b-49bd-8305-166c4c1d0dd9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362766(v=OCS.15)
ms:contentKeyID: 56271260
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Quitar un dominio de la lista de dominios permitidos

 

_**Última modificación del tema:** 2015-06-22_

Para quitar un dominio de la lista de dominios permitidos, hay que seguir varios pasos. Primero, hay que usar un comando parecido al siguiente para recuperar la colección de todos los dominios que hay actualmente en la lista:

    $x = (Get-CsTenantFederationConfiguration).AllowedDomains

Luego, se ejecuta este comando para ver los dominios:

``` 
$x
```

Tome nota de la posición numérica del dominio que quiere quitar. Si el dominio es el primero de la lista, su valor de índice es 0. Si es el segundo, el valor de índice será 1 y así sucesivamente.

Cuando sepa el número de índice, use un comando como el siguiente para quitar el dominio especificado y asegúrese de usar el número de índice correcto. Este comando quita el primer dominio de la lista (número de índice 0):

    $x.AllowedDomain.RemoveAt(0)

Finalmente, llame al cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) para escribir los cambios en Skype Empresarial Online:

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

