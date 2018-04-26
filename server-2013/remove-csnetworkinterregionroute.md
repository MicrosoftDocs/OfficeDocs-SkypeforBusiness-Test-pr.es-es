---
title: Remove-CsNetworkInterRegionRoute
TOCTitle: Remove-CsNetworkInterRegionRoute
ms:assetid: 91948c03-2bcb-4e25-b0b6-23827e85bbb3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398743(v=OCS.15)
ms:contentKeyID: 48276030
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterRegionRoute

 

_**Última modificación del tema:** 2015-03-09_

Quita una ruta que conecta regiones de red dentro de una configuración de control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En el ejemplo 1 se quita la ruta con identidad NA\_APAC\_Route.

    Remove-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## Ejemplo 2

En el ejemplo 2, se quitan todas las rutas regionales que incluyen la región NorthAmerica. La primera parte del comando es una llamada al cmdlet **Get-CsNetworkInterRegionRoute**. Este cmdlet, al que se llama sin parámetros, recupera todas las rutas regionales. Luego, esta colección de rutas se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** filtra la colección para incluir solo las rutas que tienen definida NorthAmerica como una de las regiones de la ruta. Para hacerlo, comprueba si la ruta tiene un valor de NetworkRegionID1 igual a (-eq) NorthAmerica o (-or) un valor de NetworkRegionID2 igual a NorthAmerica. Cuando la colección contiene solo las rutas que incluyen la región NorthAmerica, canalizamos la colección al cmdlet **Remove-CsNetworkInterRegionRoute**, que quita cada una de las rutas.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"} | Remove-CsNetworkInterRegionRoute

## Descripción detallada

Todas las regiones con configuraciones CAC deben tener alguna manera de obtener acceso a las demás regiones. Mientras que los vínculos regionales establecen las limitaciones de ancho de banda de las conexiones entre regiones y también representan los vínculos físicos, las rutas determinan la ruta de acceso vinculada que atravesará la conexión de una región a otra. Este cmdlet quita una de esas asociaciones de rutas.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Remove-CsNetworkInterRegionRoute** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterRegionRoute"}

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
<td><p>El identificador único de la ruta de región de red que se quiere quitar. Dado que las rutas regionales de red se crean únicamente en el ámbito global, este identificador no necesita especificar el ámbito. Por el contrario, contiene una cadena que consiste en un nombre único que identifica la ruta.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType. Acepta la entrada canalizada de objetos de ruta interregional de red.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vea también

#### Otros recursos

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

