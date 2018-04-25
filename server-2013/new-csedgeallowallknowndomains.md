---
title: New-CsEdgeAllowAllKnownDomains
TOCTitle: New-CsEdgeAllowAllKnownDomains
ms:assetid: f9416909-c328-41b3-9215-7ebd091b0ca0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994088(v=OCS.15)
ms:contentKeyID: 52061975
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowAllKnownDomains

 

_**Última modificación del tema:** 2015-03-09_

Permite la federación de Microsoft Lync Online con todos los dominios excepto con los dominios incluidos en la lista de dominios bloqueados.

Este cmdlet solo se puede usar con Skype Empresarial Online.

## Sintaxis

    New-CsEdgeAllowAllKnownDomains [-Verbose]

## Ejemplos

## Ejemplo 1

Los dos comandos del ejemplo 1 configuran las opciones de federación para el inquilino cuya identidad es "bf19b7db-6960-41e5-a139-2aa373474354" para permitir todos los dominios conocidos. Para hacer esto, el primer comando del ejemplo usa el cmdlet **New-CsEdgeAllowAllKnownDomains** para crear una instancia del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains; esta instancia se almacena en una variable denominada $x. En el segundo comando, se llama al cmdlet **Set-CsTenantFederationConfiguration** junto con el parámetro AllowedDomains; al usar $x como valor de parámetro, se configuran las opciones de federación para permitir todos los dominios conocidos.

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

## Ejemplo 2

En el ejemplo 2, se ve cómo configurar todos los inquilinos para permitir la comunicación con todos los dominios que no se muestran explícitamente en la lista de dominios bloqueados. Para hacer esto, el primer comando del ejemplo usa el cmdlet **New-CsEdgeAllowAllKnownDomains** para crear una instancia del objeto AllowAllKnownDomains, un objeto almacenado en una variable denominada $x.

Luego, el segundo comando del ejemplo usa el cmdlet **Get-CsTenant** para devolver una colección de todos los inquilinos disponibles. Luego, esta colección se canaliza al cmdlet **ForEach-Object**. El cmdlet **ForEach-Object**, a su vez, ejecuta el cmdlet **Set-CsTenantFederationConfiguration** en cada uno de los inquilinos de la colección y configura la propiedad AllowedDomains para permitir todos los dominios conocidos.

    $x = New-CsEdgeAllowAllKnownDomains
    Get-CsTenant | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantID -AllowedDomains $x}

## Descripción detallada

La federación es un servicio que permite a los usuarios intercambiar información de mensajería instantánea y presencia con usuarios de otros dominios. Con Lync Online, los administradores pueden usar las opciones de configuración de federación para controlar:

  - Si los usuarios pueden comunicarse o no con personas de otros dominios y, si pueden, con qué dominios se pueden comunicar.

  - Si los usuarios pueden comunicarse o no con personas que tienen cuentas en proveedores públicos de mensajería instantánea y de presencia, como Windows Live, AOL y Yahoo.

La federación se administra, en parte, usando listas de dominios permitidos y de dominios bloqueados. La lista de dominios permitidos recoge los dominios con los que se pueden comunicar los usuarios; la lista de dominios bloqueados recoge los dominios con los que los usuarios no se pueden comunicar. De manera predeterminada, los usuarios pueden comunicarse con cualquier dominio que no aparezca en la lista de dominios bloqueados, pero los administradores pueden modificar esta opción predeterminada y limitar la comunicación a los dominios que están en la lista de dominios permitidos.

Lync Online no le permite modificar directamente la lista de dominios permitidos o bloqueados; por ejemplo, no puede usar un comando como este, que pasa a la lista de dominios permitidos un valor de cadena que representa un nombre de dominio:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

Lo que debe hacer es usar el cmdlet **New-CsEdgeAllowAllKnownDomains** o el cmdlet **New-CsEdgeAllowList** para crear un objeto de dominio y luego pasarlo al cmdlet **Set-CsTenantFederationConfiguration**. El cmdlet **New-CsEdgeAllowAllKnownDomains** se usa si quiere permitir a los usuarios comunicarse con todos los dominios excepto con los que se recogen expresamente en la lista de dominios bloqueados. El cmdlet **ew-CsEdgeAllowList** se usa si quiere limitar la comunicación de los usuarios a una colección determinada de dominios. En este caso, los usuarios solo podrán comunicarse con los dominios que aparezcan en la lista de dominios permitidos.

Para configurar la federación con todos los dominios conocidos, use un conjunto de comandos como este:

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

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
<td><p>Este cmdlet solo presenta parámetros comunes de Windows PowerShell.</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **New-CsEdgeAllowAllKnownDomains** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **New-CsEdgeAllowAllKnownDomains** crea instancias nuevas del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains.

## Vea también

#### Otros recursos

[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

