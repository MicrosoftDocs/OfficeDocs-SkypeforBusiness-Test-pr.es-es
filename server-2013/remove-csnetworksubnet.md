---
title: Remove-CsNetworkSubnet
TOCTitle: Remove-CsNetworkSubnet
ms:assetid: 251ddb5c-4837-4810-b46f-d276f9535653
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425726(v=OCS.15)
ms:contentKeyID: 48274702
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSubnet

 

_**Última modificación del tema:** 2015-03-09_

Quita una subred de red existente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo se quita la subred con la Identidad (Id. de subred) 172.11.15.0.

    Remove-CsNetworkSubnet -Identity 172.11.15.0

## EJEMPLO 2

En el ejemplo 2 se quitan todas las subredes asociadas al sitio Vancouver. Para ello, comenzamos con una llamada del cmdlet **Get-CsNetworkSubnet**. Esto recuperará una colección de todas las subredes definidas en la implementación de Lync Server. Dicha colección de subredes se canaliza después al cmdlet **Where-Object**. El cmdlet **Where-Object** acota la colección únicamente a las subredes cuyo NetworkSiteID es igual a (-eq) Vancouver. Ahora que la colección solo incluye subredes asociadas al sitio Vancouver, canalizamos la colección al cmdlet **Remove-CsNetworkSubnet**, que quita todos los elementos de la colección.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Remove-CsNetworkSubnet

## Descripción detallada

Cada subred debe estar asociada a un sitio de red para poder determinar la ubicación geográfica del host que pertenece a esta subred. Use este cmdlet para quitar una subred de red.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsNetworkSubnet** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSubnet"}

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
<td><p>Id. de subred único de la subred que se quiere quitar. Este valor será una dirección IP (por ejemplo, 174.11.12.0).</p></td>
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
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType. Acepta entradas canalizadas de objetos de subred de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Vea también

#### Otros recursos

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

