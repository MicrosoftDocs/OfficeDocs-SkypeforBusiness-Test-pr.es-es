---
title: Remove-CsNetworkRegionLink
TOCTitle: Remove-CsNetworkRegionLink
ms:assetid: f26cde90-e789-44a7-a304-695c85e64403
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg413012(v=OCS.15)
ms:contentKeyID: 48277148
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegionLink

 

_**Última modificación del tema:** 2015-03-09_

Quita un vínculo entre dos regiones configuradas para el control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este primer ejemplo quita el vínculo de región de red con el valor de Identity NA\_EMEA.

    Remove-CsNetworkRegionLink -Identity NA_EMEA

## Ejemplo 2

El ejemplo 2 quita todos los vínculos de región de red que usan el perfil de directiva de ancho de banda llamado HighBWLimits. El primer cmdlet al que se llama en el ejemplo es el cmdlet **Get-CsNetworkRegionLink** (sin ningún parámetro), que recupera todos los vínculos de región. A continuación, esta recopilación de vínculos se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** examina los elementos de la recopilación, uno por uno, para comprobar el valor de la propiedad BWPolicyProfileID. Si esta propiedad es igual a (-eq) HighBWLimits, el elemento se canaliza al cmdlet **Remove-CsNetworkRegionLink**, que quita el vínculo.

    Get-CsNetworkRegionLink | Where-Object {$_.BWPolicyProfileID -eq "HighBWLimits"} | Remove-CsNetworkRegionLink

## Descripción detallada

Las regiones de una red se vinculan mediante conexiones de red WAN físicas. Este cmdlet no afecta a las conexiones físicas, solo quita el vínculo de la configuración de CAC.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **Remove-CsNetworkRegionLink** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegionLink"}

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
<th>Requerido</th>
<th>Tipo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Requerido</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>El identificador único del vínculo de región de red que quiere quitar. Los vínculos de región de red solo pueden crearse en el ámbito global, por lo tanto, no es necesario especificar un ámbito en este identificador. En su lugar, contiene una cadena de caracteres que consiste en el nombre único que identifica dicho vínculo.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType. Acepta la entrada por canalización de objetos de vínculo de región de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vea también

#### Otros recursos

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

