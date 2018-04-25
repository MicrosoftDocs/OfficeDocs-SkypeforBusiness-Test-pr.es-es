---
title: Habilitar o deshabilitar un proveedor de mensajería instantánea pública específico
TOCTitle: Habilitar o deshabilitar un proveedor de mensajería instantánea pública específico
ms:assetid: 9d3e2607-01c0-4ae9-accc-39f03ce253bb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362825(v=OCS.15)
ms:contentKeyID: 56271331
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Habilitar o deshabilitar un proveedor de mensajería instantánea pública específico

 

_**Última modificación del tema:** 2015-06-22_

Skype Empresarial Online le permite establecer federación con usuarios de uno o más de los siguientes proveedores de mensajería instantánea (MI) pública:

  - Red de Windows Live de servicios de Internet

  - Yahoo\!

  - AOL

Para permitir la federación con uno o más de estos proveedores, use el cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) y establezca el valor de la propiedad Provider en uno o más de estos valores:

  - Windows Live

  - Yahoo\!

  - AOL

Por ejemplo, este comando establece federación con Windows Live y AOL:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Tenga en cuenta que, cuando quiera agregar o quitar un proveedor, debe incluir en el comando todos los proveedores federados relevantes. Por ejemplo, agregue Yahoo\! y ejecute este comando:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo"

El comando dejará Yahoo\! como el único proveedor federado, porque es el que se llamó. Para establecer federación con los tres proveedores de MI pública, debe incluirlos todos:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo", "AOL","WindowsLive"

Tenga en cuenta que debe incluir el parámetro Tenant al llamar al cmdlet Set-CsTenantPublicProvider. Si no lo hace, se le pedirá que especifique el identificador de inquilino. Para devolver el identificador de inquilino de su inquilino de Skype Empresarial Online, use este comando:

    Get-CsTenant | Select-Object TenantID

O bien use este comando para almacenar el identificador de inquilino en una variable:

    $tenantID = (Get-CsTenant | Select-Object TenantID)

Puede usar esa variable (en este ejemplo, $tenantID) al llamar a Set-CsTenantPublicProvider:

    Set-CsTenantPublicProvider -Tenant $tenantID -Provider "Yahoo", "AOL","WindowsLive"

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

