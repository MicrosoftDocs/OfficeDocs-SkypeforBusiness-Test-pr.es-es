---
title: New-CsNetworkRegionLink
TOCTitle: New-CsNetworkRegionLink
ms:assetid: 61a6a7be-8078-4d59-a78a-2f241f6bf800
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398437(v=OCS.15)
ms:contentKeyID: 48275453
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegionLink

 

_**Última modificación del tema:** 2015-03-09_

Crea un vínculo entre dos regiones configuradas para el control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsNetworkRegionLink -NetworkRegionLinkID <String> <COMMON PARAMETERS>

    New-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo se crea un nuevo vínculo de región de red denominado NA\_EMEA para vincular las regiones de NorthAmerica y EMEA. El nombre de vínculo de región se especifica como valor para el parámetro Identity (se asigna de forma automática como valor del parámetro NetworkRegionLinkID). Las dos regiones de red que se vinculan son parámetros necesarios para crear el vínculo (en este caso, NorthAmerica y EMEA). En este ejemplo también se asigna un valor al parámetro BWPolicyProfile, que asigna las limitaciones de ancho de banda del perfil de directiva de ancho de banda (LowBWLimits) a las conexiones existentes entre estas regiones. Si no se proporciona BWPolicyProfileID, no se establece ninguna limitación de ancho de banda para las conexiones entre estas dos regiones. No obstante, es posible que haya limitaciones entre sitios específicos. Para más información, vea el tema de Ayuda del cmdlet **New-CsNetworkSite**.

    New-CsNetworkRegionLink -Identity NA_EMEA -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID LowBWLimits

## Descripción detallada

Regiones dentro de una red que se enlazan a través de conectividad WAN física. Este cmdlet define un vínculo entre dos regiones y establece los límites de ancho de banda en las conexiones de audio y vídeo entre estas regiones.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **New-CsNetworkRegionLink** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegionLink"}

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
<td><p>Un identificador único para el vínculo de región de red creado recientemente. Los vínculos de región de red se crean solo en el ámbito global; por lo tanto, este identificador no necesita especificar un ámbito. En cambio, contiene una cadena que es un nombre único que identifica ese vínculo.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>La Identidad (NetworkRegionID) de la región que se enlaza a la región identificada por el parámetro NetworkRegionID2.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>La Identidad (NetworkRegionID) de la región que se enlaza a la región identificada por el parámetro NetworkRegionID1.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkID</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>El valor es el mismo que el valor Identity. No puede especificar una Identidad y un NetworkRegionLinkID; un valor ingresado para uno se usará para los dos de manera automática.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>La Identidad del perfil de la directiva de ancho de banda que define los límites de ancho de banda para este vínculo. Puede recuperar una lista de los perfiles disponibles llamando al cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
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
<td><p>Suprime las solicitudes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Este cmdlet crea un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vea también

#### Otros recursos

[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkSite](new-csnetworksite.md)

