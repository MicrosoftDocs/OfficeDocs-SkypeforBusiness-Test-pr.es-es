---
title: Get-CsNetworkInterRegionRoute
TOCTitle: Get-CsNetworkInterRegionRoute
ms:assetid: 31c38d92-1cef-40fe-bd04-26e5b373703e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425817(v=OCS.15)
ms:contentKeyID: 48274849
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterRegionRoute

 

_**Última modificación del tema:** 2015-03-09_

Recupera una ruta o más que conectan las regiones de red dentro de una configuración de control de admisión de llamadas (CAC, call admission control). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterRegionRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

El Ejemplo 1 recupera la ruta con el valor Identity NA\_APAC\_Route.

    Get-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## EJEMPLO 2

En el ejemplo 2, usamos el parámetro Filter para recuperar todas las rutas que contienen la cadena APAC en cualquier lugar dentro del valor Identity.

    Get-CsNetworkInterRegionRoute -Filter *APAC*

## EJEMPLO 3

Este ejemplo recupera todas las rutas de región que usan el vínculo de región de red NA\_EMEA. En primer lugar, el comando llama al cmdlet **Get-CsNetworkInterRegionRoute**. Al llamar a este cmdlet sin parámetros se recuperan todas las rutas definidas con la configuración de CAC. A continuación, esta colección de rutas se canaliza al cmdlet **Where-Object**. **Where-Object** recibe la colección y recupera todos los elementos de esta que tienen el valor NA\_EMEA en su lista NetworkRegionLinks.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionLinks -eq "NA_EMEA"}

## EJEMPLO 4

El Ejemplo 4 recupera todas las rutas de región que incluyan la región NorthAmerica. La primera parte del comando consiste en un llamado al cmdlet **Get-CsNetworkInterRegionRoute**. Este cmdlet, al que se llama sin parámetros, recuperará todas las rutas de región. A continuación, esta recopilación de rutas se redirecciona al cmdlet **Where-Object**. El cmdlet **Where-Object** limitará la recopilación para incluir solo las rutas que tienen definida NorthAmerica como una de las regiones de la ruta. Realiza esto controlando si la ruta tiene un valor NetworkRegionID1 igual a (-eq) NorthAmerica o (-or) un valor NetworkRegionID2 igual a NorthAmerica.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"}

## Descripción detallada

Cada región dentro de una configuración CAC debe tener alguna forma de obtener acceso a todas las otras regiones. Mientras que los vínculos regionales establecen las limitaciones de ancho de banda de las conexiones entre regiones y también representan los vínculos físicos, las rutas determinan las vías de acceso vinculadas por las que se desplazará la conexión al pasar de una región a otra. Este cmdlet recupera información sobre estas asociaciones de rutas.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar el cmdlet **Get-CsNetworkInterRegionRoute** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterRegionRoute"}

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
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Una cadena que le permite recuperar rutas basándose en la coincidencia de los valores Identity con la cadena con comodín transferida como un valor para este parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>El identificador único para la ruta de región de red que quiere recuperar. Las rutas de región de red se crean solo en el ámbito global; por lo tanto, no es necesario que este identificador especifique un ámbito. Por el contrario, contiene una cadena que consiste en un nombre único que identifica una ruta particular.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información de ruta interregional de red de la réplica local de la Almacén de administración central, en lugar de la Almacén de administración central en sí.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Este cmdlet devuelve uno o más objetos tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vea también

#### Otros recursos

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

