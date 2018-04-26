---
title: Permitir la federación con todos los dominios
TOCTitle: Permitir la federación con todos los dominios
ms:assetid: d26f1057-a76c-447a-9efe-72efdce4c15e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362855(v=OCS.15)
ms:contentKeyID: 56271359
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Permitir la federación con todos los dominios

 

_**Última modificación del tema:** 2015-06-22_

Si desea que los usuarios puedan comunicarse con otros usuarios de cualquier dominio, debe realizar dos tareas. En primer lugar, cree una instancia del objeto AllowAllKnownDomains con el cmdlet [New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md):

    $x = New-CsEdgeAllowAllKnownDomains

A continuación, llame al cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) y establezca el valor de la propiedad AllowedDomains en la variable que contiene el objeto AllowAllKnownDomains ($x en este ejemplo):

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

