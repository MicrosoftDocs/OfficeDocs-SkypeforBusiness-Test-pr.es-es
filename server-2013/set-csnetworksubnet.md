---
title: Set-CsNetworkSubnet
TOCTitle: Set-CsNetworkSubnet
ms:assetid: 9e85cdbb-b5fb-48d6-8f95-6e7cba9d9597
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412739(v=OCS.15)
ms:contentKeyID: 48276152
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSubnet

 

_**Última modificación del tema:** 2015-03-09_

Modifica una subred de red existente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSubnet [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaskBits <Int32>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo, se modifica la subred con identidad (identificador de subred) 172.11.15.0. La subred se modifica con un nuevo valor de MaskBits (25) y un nuevo NetworkSiteID (Chicago).

    Set-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 25 -NetworkSiteID Chicago

## Ejemplo 2

En el ejemplo 2, se mueven todas las subredes del sitio de Vancouver al sitio de Chicago. Para ello, primero se llama al cmdlet **Get-CsNetworkSubnet**. Se recupera una colección de todas las subredes definidas en la implementación de Lync Server. Después, la colección de subredes se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** filtra la colección para obtener únicamente las subredes con NetworkSiteID igual a (-eq) Vancouver. Ahora que la colección solo se compone de subredes asociadas con el sitio de Vancouver, canalizamos la colección al cmdlet **Set-CsNetworkSubnet**. Suministramos un parámetro al cmdlet **Set-CsNetworkSubnet**: NetworkSiteID. Al pasarle al parámetro el valor de Chicago, le volvemos a indicar al cmdlet **Set-CsNetworkSubnet** que cambie el identificador del sitio de red de cada miembro de la colección a Chicago.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Set-CsNetworkSubnet -NetworkSiteID Chicago

## Descripción detallada

Cada subred debe estar asociada a un sitio de red a fin de determinar la ubicación geográfica del host que pertenece a esta subred. Use este cmdlet para modificar el sitio de red asociado, cambiar la descripción de la subred o modificar los bits de máscara de la subred.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **Set-CsNetworkSubnet** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSubnet"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Descripción de la subred que se modifica.</p></td>
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
<td><p>El identificador de subred único de la subred que desea modificar. Este valor será una dirección IP (por ejemplo, 174.11.12.0) o una URL que comience con http: o https:.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>SubnetType</p></td>
<td><p>Referencia a un objeto de subred de la red que quiere modificar. Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType, que se puede recuperar al llamar al cmdlet <strong>Get-CsNetworkSubnet</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>La máscara de bits que se aplicará a la subred.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>El identificador del sitio correspondiente al sitio de red en que se aplicará esta subred. Puede recuperar los Id. de sitio de la implementación llamando al cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType. Acepta la entrada canalizada de los objetos de la subred de red.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Vea también

#### Otros recursos

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

