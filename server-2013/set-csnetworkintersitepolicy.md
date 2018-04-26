---
title: Set-CsNetworkInterSitePolicy
TOCTitle: Set-CsNetworkInterSitePolicy
ms:assetid: 973979bc-db2c-47a6-909e-5949a927f51c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398772(v=OCS.15)
ms:contentKeyID: 48276085
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterSitePolicy

 

_**Última modificación del tema:** 2015-03-09_

Modifica una directiva entre sitios de red existente que define las limitaciones de ancho de banda entre sitios que estén vinculados directamente dentro de una configuración de control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterSitePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkSiteID1 <String>] [-NetworkSiteID2 <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este ejemplo modifica la directiva de sitios de red con Identity Reno\_Portland. Usamos el parámetro BWPolicyProfileID para cambiar el perfil de directiva de ancho de banda asociado con esta directiva de sitios de red a HighBWLimits.

    Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

## Descripción detallada

Cuando los sitios de red comparten un vínculo directo, se pueden definir las limitaciones de ancho de banda de las conexiones de audio y vídeo entre ambos sitios. Este cmdlet modifica una directiva entre sitios de red que asocia una directiva de límite de ancho de banda con dos sitios conectados directamente.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para iniciar el cmdlet **Set-CsNetworkInterSitePolicy** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterSitePolicy"}

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
<td><p>La identidad del perfil de directiva de ancho de banda que definirá las limitaciones de esta directiva de sitios. Puede recuperar una lista de los perfiles disponibles si llama al cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>.SwitchParameter</p></td>
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
<td><p>El identificador único de la directiva de sitios de red que se desea modificar. Dado que las directivas de sitios de red se crean únicamente en el ámbito global, este identificador no necesita especificar el ámbito. Por el contrario, contiene una cadena que consiste en un nombre único que identifica la directiva del sitio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>InterNetworkSitePolicyType</p></td>
<td><p>Referencia de objeto a una directiva de sitios que se ha modificado en la memoria. Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType y se puede recuperar si se llama al cmdlet <strong>Get-CsNetworkInterSitePolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La identidad (NetworkSiteID) de uno de los dos sitios asociados a la directiva. La combinación de NetworkSiteID1 y NetworkSiteID2 debe ser única (por ejemplo, no se pueden definir dos directivas de sitio que conecten Reno y Portland).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La identidad (NetworkSiteID) de uno de los dos sitios asociados a la directiva. La combinación de NetworkSiteID1 y NetworkSiteID2 debe ser única (por ejemplo, no se pueden definir dos directivas de sitio que conecten Reno y Portland).</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType. Acepta la entrada canalizada de objetos de directiva entre sitios de red.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Vea también

#### Otros recursos

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

