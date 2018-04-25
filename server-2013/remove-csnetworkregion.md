---
title: Remove-CsNetworkRegion
TOCTitle: Remove-CsNetworkRegion
ms:assetid: 661dce40-f601-4181-b8f1-3277a76d5df4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398466(v=OCS.15)
ms:contentKeyID: 48275492
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegion

 

_**Última modificación del tema:** 2015-03-09_

Quita una región de red existente. Las regiones de red representan redes troncales o concentradores de red de una red empresarial. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se quita la región de red con Identidad NorthAmerica. Dado que las identidades son únicas, este comando quita solo una región de red.

    Remove-CsNetworkRegion -Identity NorthAmerica

## EJEMPLO 2

En este ejemplo se quitan todas las regiones de red que se han asociado con el sitio central Redmond. En primer lugar, el llama al cmdlet **Get-CsNetworkRegion** sin ningún parámetro, para recuperar una colección de todas las regiones de red que se han definido para la implementación de Lync Server. A continuación, esta colección se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** filtra esta colección para devolver solamente aquellos elementos (regiones de red) cuyo valor de CentralSite es igual a (-eq) site:Redmond. Tras restringir la colección a estos elementos, se canaliza al cmdlet **Remove-CsNetworkRegion**, que quita los distintos elementos de la colección.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"} | Remove-CsNetworkRegion

## EJEMPLO 3

En este ejemplo se quita la región de red con Identidad NorthAmerica. No obstante, no se puede quitar una región si está asociada a un sitio. De modo que este ejemplo quita primero cualquier asociación entre la región NorthAmerica y un sitio.

En primer lugar, en el ejemplo se llama al cmdlet **Get-CsNetworkSite** sin ningún parámetro, para recuperar una colección con todos los sitios de red que se han definido para la implementación de Lync Server. A continuación, esta colección se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** filtra esta colección para devolver solo aquellos elementos (sitios de red) cuyo valor de NetworkRegionID es igual a (-eq) NorthAmerica. Tras restringir la colección a estos elementos, se canaliza al cmdlet **Set-CsNetworkSite**. En todos los sitios cuyo valor de NetworkRegionID es NorthAmerica, se establece el parámetro NetworkRegionID en Null ($null). De esta forma, se quitan las referencias a las regiones en estos sitios. Sin embargo, un sitio no puede tener un identificador de omisión si no se ha asociado con otro sitio. De modo que, además de establecer NetworkRegionID en Null para quitar la referencia a la región, también debe establecer BypassID en Null para quitar la asociación de omisión.

Una vez finalizada la línea 1, cualquier sitio que estuviera asociado a la región NorthAmerica deja de estar vinculado a una región o a una configuración de desvío. A continuación podemos llamar a la línea 2, que quita la región de red.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"} | Set-CsNetworkSite -NetworkRegionID $null -BypassID $null
    Remove-CsNetworkRegion -Identity "NorthAmerica"

## Descripción detallada

Una región de red interconecta varias partes de una red en varias zonas geográficas. Cada región de red debe estar asociada a un sitio central. El sitio central es el sitio del centro de datos donde se ejecuta el servicio de directiva de ancho de banda. Use este cmdlet para quitar una región de red.

Tenga en cuenta que no se puede quitar una región de red si está asociada a un sitio de red (es decir, si la propiedad NetworkRegionID de un sitio es igual a la propiedad Identity de la región). Si intenta quitar una región asociada a un sitio, recibirá un mensaje de error.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsNetworkRegion** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegion"}

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
<td><p>El identificador único de la región de red que se quiere quitar. La Identidad estará representada por una cadena que identifique la región de forma única.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType. Acepta entradas canalizadas de objetos de región de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vea también

#### Otros recursos

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

