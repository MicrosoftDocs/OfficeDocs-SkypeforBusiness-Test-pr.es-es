---
title: Remove-CsNetworkBandwidthPolicyProfile
TOCTitle: Remove-CsNetworkBandwidthPolicyProfile
ms:assetid: 7b1f3c8d-486c-4a7e-aa40-57893f249f66
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398609(v=OCS.15)
ms:contentKeyID: 48275769
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkBandwidthPolicyProfile

 

_**Última modificación del tema:** 2015-03-09_

Quita un perfil de directiva del ancho de banda de red. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo, se quita el perfil de directivas de ancho de banda con la identidad LowBWProfile. Debido a que las identidades deben ser únicas quitará, como mucho, un perfil.

    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## Ejemplo 2

En el ejemplo 2 todas las referencias al perfil de directivas de ancho de banda con identidad LowBWProfile se quitan de todos los sitios al que ha sido asignado; después, se quita ese perfil. La primera línea de este ejemplo empieza con una llamada al cmdlet **Get-CsNetworkSite** para recuperar todos los sitios configurados para el servicio de control de admisión de llamadas (CAC). Esta recopilación de sitios después se canaliza al cmdlet **Where-Object**, que busca solo aquellos sitios con BWPolicyProfileID igual a (-eq) LowBWProfile. Esta recopilación reducida, que solo contiene sitios con un valor BWPolicyProfileID de LowBWProfile, se canaliza al cmdlet **Set-CSNetworkSite**, que modifica cada uno de estos sitios para cambiar BWPolicyProfileID a nulo ($null). Lo que acabamos de hacer es encontrar todos los sitios con BWPolicyProfileID de LowBWProfile y configurar ese valor en nulo. En este punto no hay sitios que usen el perfil LowBWProfile. Ahora llamamos al cmdlet **Remove-CsNetworkBandwidthPolicyProfile** en el perfil LowBWProfile para eliminar el perfil, sabiendo que el perfil no está en uso por parte de ningún sitio.

Para garantizar que el perfil no está en uso en ninguna ubicación de la configuración de red, realice los mismos procedimientos en la Línea 1 según directivas entre sitios y vínculos de región de red.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Set-CsNetworkSite -BWPolicyProfileID $null
    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## Descripción detallada

Como parte del control de admisión de llamadas (CAC), se usa una directiva de ancho de banda para definir las limitaciones de ancho de banda para ciertas modalidades. (En Lync Server, solo se pueden asignar limitaciones de ancho de banda a las modalidades de audio y vídeo). El cmdlet quita el perfil contenedor de estas directivas.

IMPORTANTE: Si se ha asignado un perfil a un sitio (con el cmdlet **New-CsNetworkSite** o el cmdlet **Set-CsNetworkSite**), a una directiva entre sitios (con el cmdlet **New-CsNetworkInterSitePolicy** o el cmdlet **Set-CsNetworkInterSitePolicy**), o a un vínculo de región de red (con el cmdlet **New-CsNetworkRegionLink** o el cmdlet **Set-CsNetworkRegionLink**), no se podrá quitar. Recibirá un mensaje de error si intenta quitar el perfil al llamar al cmdlet **Remove-CsNetworkBandwidthPolicyProfile**. Primero debe quitar el perfil de todos los sitios, directivas entre sitios y vínculos de región de red y, después, podrá quitar el perfil.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para iniciar el cmdlet **Remove-CsNetworkBandwidthPolicyProfile** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Valor de cadena que identifica de manera única el perfil de directivas de ancho de banda que desea quitar. Si especifica una identidad quitará, como mucho, un perfil.</p></td>
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
<td><p>Suprime las preguntas de confirmación que aparecen antes de hacer cambios.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType. Acepta la entrada canalizada de objetos de perfil de directiva de ancho de banda de red.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vea también

#### Otros recursos

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

