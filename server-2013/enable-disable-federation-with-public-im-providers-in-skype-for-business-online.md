---
title: Habilitar o deshabilitar la federación con los proveedores de mensajería instantánea pública
TOCTitle: Habilitar o deshabilitar la federación con los proveedores de mensajería instantánea pública
ms:assetid: 8609682c-97d3-48e6-a243-d84c1f9c8419
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362809(v=OCS.15)
ms:contentKeyID: 56271298
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Habilitar o deshabilitar la federación con los proveedores de mensajería instantánea pública

 

_**Última modificación del tema:** 2015-06-22_

Para permitir que sus usuarios se comuniquen con otros que tienen cuentas en un proveedor de mensajería instantánea (MI) pública, use el cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) y establezca la propiedad AllowPublicUsers en True ($True):

    Set-CsTenantFederationConfiguration -AllowPublicUsers $True

Tenga en cuenta que tiene que usar el cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) para especificar los proveedores de MI pública con los que los usuarios podrán comunicarse.

Para deshabilitar la federación con proveedores públicos, vuelva a establecer la propiedad AllowPublicUsers en False ($False):

    Set-CsTenantFederationConfiguration -AllowPublicUsers $False

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

