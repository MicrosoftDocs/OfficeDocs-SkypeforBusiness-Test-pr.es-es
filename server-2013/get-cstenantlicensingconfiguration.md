---
title: Get-CsTenantLicensingConfiguration
TOCTitle: Get-CsTenantLicensingConfiguration
ms:assetid: 0df23143-f1aa-4850-b0f7-750422762925
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362770(v=OCS.15)
ms:contentKeyID: 56271265
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantLicensingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Indica si la información de licencia del inquilino especificado está disponible en el Centro de administración de Lync.

Este cmdlet solo se puede usar con Lync Online.

## Sintaxis

    Get-CsTenantLicensingConfiguration [-Filter] <Object>] [-Identity] <Object>] [-Tenant] <Object>] [-LocalStore]

## Descripción detallada

El cmdlet Get-CsTenantLicensingConfiguration indica si la información de licencia del inquilino especificado está disponible en el Centro de administración de Lync. El cmdlet devuelve información que se parece a esto:

Identity : Global  
Status : Enabled

Si el estado es igual a Enabled (habilitado), la información de licencia está disponible en el Centro de administración de Lync. Si no, esta información no está disponible en el Centro de administración de Lync.

## Parámetros


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Obligatorio</th>
<th>Tipo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Filter</strong></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite usar caracteres comodines para devolver una colección de opciones de configuración de licencia de inquilino. Como cada parámetro se limita a una sola colección global de opciones de configuración de licencia, no hay necesidad de usar el parámetro Filter.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Especifica la colección de opciones de configuración de licencia del inquilino que se debe devolver. Como cada parámetro se limita a una sola colección global de opciones de configuración de licencia, no hay necesidad de incluir este parámetro al llamar al cmdlet Get-CsTenantLicensingConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalStore</strong></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración de la licencia de inquilino desde la réplica local del Almacén de administración central en lugar de hacerlo desde el propio Almacén de administración central.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tenant</strong></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuya configuración de licencia se quiere devolver. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el identificador de inquilino de cada uno de los inquilinos ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

El cmdlet Get-CsTenantLicensingConfiguration no acepta entradas de canalización.

## Tipos de valores devueltos

El cmdlet Get-CsTenantLicensingConfiguration cmdlet devuelve instancias del objeto Deserialized.Microsoft.Rtc.Management.WritableConfig.Settings.TenantConfiguration.TenantLicensingConfiguration.

## Ejemplo

El comando del ejemplo 1 devuelve la información de configuración de licencia del inquilino actual:

    Get-CsTenantLicensingConfiguration

