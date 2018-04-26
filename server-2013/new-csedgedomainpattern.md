---
title: New-CsEdgeDomainPattern
TOCTitle: New-CsEdgeDomainPattern
ms:assetid: 653bc148-c22b-4ad4-afdd-17aaeaa299d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994040(v=OCS.15)
ms:contentKeyID: 52061695
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeDomainPattern

 

_**Última modificación del tema:** 2015-03-09_

Se usa para especificar un dominio que se agregará o quitará del conjunto de dominios habilitados o deshabilitados para la federación. Tiene que usar el cmdlet **New-CsEdgeDomainPattern** al modificar las listas de dominios permitidos o bloqueados. Los valores de cadena (como "fabrikam.com") no se pueden pasar directamente a los cmdlets usados para administrar estas listas.

El cmdlet **New-CsEdgeDomainPattern** solo se puede usar con Skype Empresarial Online.

## Sintaxis

    New-CsEdgeDomainPattern -Domain <String> [-Verbose]

## Ejemplos

## Ejemplo 1

En el ejemplo 1, se ve cómo asignar un solo dominio a la lista de dominios bloqueados para un inquilino especificado. Para hacerlo, el primer comando del ejemplo crea un objeto de dominio para el dominio fabrikam.com; esto se hace llamando al cmdlet **New-CsEdgeDomainPattern** y guardando el objeto de dominio resultante en una variable denominada $x. Luego, el segundo comando usa el cmdlet **Set-CsTenantFederationConfiguration** y el parámetro BlockedDomains para configurar fabrikam.com como el único dominio bloqueado por el inquilino cuyo TenantId es "bf19b7db-6960-41e5-a139-2aa373474354".

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

## Descripción detallada

La federación es un servicio que permite a los usuarios intercambiar información de mensajería instantánea y presencia con usuarios de otros dominios. Con Skype Empresarial Online, los administradores pueden usar las opciones de configuración de federación para controlar:

  - Si los usuarios pueden comunicarse o no con personas de otros dominios y, si pueden, con qué dominios se pueden comunicar.

  - Si los usuarios pueden comunicarse o no con personas que tienen cuentas en proveedores públicos de mensajería instantánea y de presencia, como Windows Live, AOL y Yahoo.

La federación se administra, en parte, usando listas de dominios permitidos y de dominios bloqueados. La lista de dominios permitidos recoge los dominios con los que se pueden comunicar los usuarios; la lista de dominios bloqueados recoge los dominios con los que los usuarios no se pueden comunicar. De manera predeterminada, los usuarios pueden comunicarse con cualquier dominio que no aparezca en la lista de dominios bloqueados, pero los administradores pueden modificar esta opción predeterminada y limitar la comunicación a los dominios que están en la lista de dominios permitidos.

Skype Empresarial Online no le permite modificar directamente la lista de dominios permitidos o bloqueados; por ejemplo, no puede usar un comando como este, que pasa a la lista de dominios bloqueados un valor de cadena que representa un nombre de dominio:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains "fabrikam.com"

Lo que debe hacer es crear un objeto de dominio usando el cmdlet **New-CsEdgeDomainPattern**, almacenarlo en una variable (en este ejemplo, $x) y luego pasar el nombre de variable a la lista de dominios bloqueados:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

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
<td><p><em>Domain</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de dominio completo del dominio que se va a agregar a la lista de permitidos. Por ejemplo:</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>Recuerde que no puede usar caracteres comodín para especificar un nombre de dominio.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **New-CsEdgeDomainPattern** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **New-CsEdgeDomainPattern** crea nuevas instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DomainPattern.

## Vea también

#### Otros recursos

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

