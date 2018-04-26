---
title: Set-CsNetworkRegionLink
TOCTitle: Set-CsNetworkRegionLink
ms:assetid: b3d5d203-2aa7-4a54-93d4-30bcda391d68
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412867(v=OCS.15)
ms:contentKeyID: 48276409
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegionLink

 

_**Última modificación del tema:** 2015-03-09_

Modifica el vínculo entre dos regiones de red configuradas para el control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegionLink [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este ejemplo cambia el perfil de directiva de ancho de banda del vínculo regional de red denominado NA\_EMEA por el perfil HighBWLimits. El nombre del vínculo regional de red que se desea modificar se especifica como el valor de parámetro Identity. A continuación, se ha asignado el valor HighBWLimits al parámetro BWPolicyProfile. Esto asignará las limitaciones de ancho de banda definidas en este perfil de directiva de ancho de banda (HighBWLimits) para conexiones entre estas regiones.

    Set-CsNetworkRegionLink -Identity NA_EMEA -BWPolicyProfileID HighBWLimits

## Descripción detallada

Las regiones incluidas en una red están vinculadas a través de una conexión WAN física. Este cmdlet modifica un vínculo existente entre dos regiones, permitiendo así cambiar cualquiera de las regiones vinculadas, así como las limitaciones de ancho de banda de conexiones de audio y vídeo entre estas regiones.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsNetworkRegionLink** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegionLink"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La identidad del perfil de directiva de ancho de banda que definirá las limitaciones de este vínculo. Puede recuperar una lista de los perfiles disponibles llamando al cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecen antes de hacer cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>El único identificador del vínculo regional de red que desee modificar. Dado que los vínculos regionales de red se crean únicamente en el ámbito global, este identificador no necesita especificar el ámbito. Por el contrario, contiene una cadena que consiste en un nombre único que identifica el vínculo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>NetworkRegionLinkType</p></td>
<td><p>Una referencia de objeto a un vínculo regional de red. Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType, que se puede recuperar llamando al cmdlet <strong>Get-CsNetworkRegionLink</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La identidad (NetworkRegionID) de la región que está vinculada a la región identificada por la propiedad NetworkRegionID2.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La identidad (NetworkRegionID) de la región que está vinculada a la región identificada por la propiedad NetworkRegionID1.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType. Acepta la entrada canalizada de objetos de vínculo regional de red.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vea también

#### Otros recursos

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

