---
title: Set-CsNetworkInterRegionRoute
TOCTitle: Set-CsNetworkInterRegionRoute
ms:assetid: 5d9da3c0-56fc-401d-baf3-ed6c0f50f53d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398410(v=OCS.15)
ms:contentKeyID: 48275413
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterRegionRoute

 

_**Última modificación del tema:** 2015-03-09_

Modifica una ruta existente que conecta las regiones de red dentro de una configuración de control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterRegionRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

Este ejemplo modifica la ruta NA\_APAC\_Route al cambiar los vínculos de región que se recorrerán en la ruta. El parámetro NetworkRegionLinkIDs se usa con un valor de “NA\_SA,SA\_APAC”, que reemplaza todos los vínculos existentes con el especificado en esa cadena.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## EJEMPLO 2

Como el ejemplo 1, el ejemplo 2 modifica los vínculos dentro de la ruta NA\_APAC\_Route. No obstante, en este ejemplo, en lugar de reemplazar todos los vínculos para esa ruta mediante el parámetro NetworkRegionLinkIDs, se usa el parámetro NetworkRegionLinks para agregar un vínculo a la lista de vínculos que ya existen en esa ruta. En este caso, el vínculo SA\_EMEA se agrega a la ruta. La sintaxis @{add=\<link\>} agrega un elemento a la lista de vínculos. Además, puede usar la sintaxis @{replace=\<link\>} para reemplazar los vínculos existentes por aquellos especificados por \<vínculo\> (que, esencialmente, se comporta de la misma manera que si se usa NetworkRegionLinkIDs) o la sintaxis @{remove=\<link\>} para quitar un vínculo de la lista.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinks @{add="SA_EMEA"}

## EJEMPLO 3

En el ejemplo 3 modifica la ruta denominada NA\_Route5. Este ejemplo cambia una de las regiones que forman esta ruta. El parámetro NetworkRegionID2 se usa para especificar una nueva región, y por lo tanto, el parámetro NetworkRegionLinkIDs se usa para crear una nueva lista de vínculos que conectan las regiones de esta ruta.

    Set-CsNetworkInterRegionRoute -Identity NA_Route5 -NetworkRegionID2 SouthAmerica -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## Descripción detallada

Cada región dentro de una configuración CAC debe tener alguna forma de obtener acceso a todas las otras regiones. Mientras que los vínculos regionales establecen las limitaciones de ancho de banda de las conexiones entre regiones y además representan los vínculos físicos, las rutas determinan la ruta de acceso vinculada que atravesará la conexión de una región a otra. Este cmdlet modifica esa asociación de rutas.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsNetworkInterRegionRoute** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterRegionRoute"}

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
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las solicitudes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>El identificador único de la ruta de región de red que se desea modificar. Las rutas de región de red se crean solo en el ámbito global; por lo tanto, no es necesario que este identificador especifique un ámbito. En cambio, contiene una cadena que es un nombre único que identifica esa ruta.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>InterNetworkRegionRouteType</p></td>
<td><p>Una referencia de objeto a una ruta de región existente. Este objeto debe ser del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType, que se puede recuperar al llamar al cmdlet <strong>Get-CsNetworkInterRegionRoute</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La Identity (NetworkRegionID) de una de las dos regiones conectadas a través de esta ruta. El valor pasado a este parámetro debe ser una región diferente del valor de parámetro NetworkRegionID2. (En otras palabras, no se puede enrutar una región a sí misma). Además, la combinación de NetworkRegionID1 y NetworkRegionID2 debe ser única (por ejemplo, no puede tener dos rutas definidas que conecten NorthAmerica y EMEA).</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La Identity (NetworkRegionID) de una de las dos regiones conectadas a través de esta ruta. El valor pasado a este parámetro debe ser una región diferente del valor de parámetro NetworkRegionID1. (En otras palabras, no se puede enrutar una región a sí misma). Además, la combinación de NetworkRegionID1 y NetworkRegionID2 debe ser única (por ejemplo, no puede tener dos rutas definidas que conecten NorthAmerica y EMEA).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Permite especificar todos los vínculos para esta ruta como una cadena de valores separados por coma. Los valores son las identidades (NetworkRegionLinkIDs) de los vínculos de región. Si escribe valores para ambos parámetros, NetworkRegionLinkIDs y NetworkRegionLinks, no se tendrá en cuenta NetworkRegionLinkIDs. Todos los vínculos modificados con este parámetro remplazarán todos los vínculos existentes en la ruta.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un objeto de lista que contiene las identidades (NetworkRegionLinkIDs) de los vínculos de región que se aplican a esta ruta. Para este cmdlet, este parámetro difiere de NetworkRegionLinkIDs en que, además de permitirle remplazar todos los vínculos existentes para esta ruta, usted puede agregar o quitar vínculos específicos.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType. Acepta entradas transferidas de objetos de ruta interregional de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vea también

#### Otros recursos

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

