---
title: Get-CsNetworkRegion
TOCTitle: Get-CsNetworkRegion
ms:assetid: 5c9eef10-16c1-45f7-ae7b-2bee0965b421
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398406(v=OCS.15)
ms:contentKeyID: 48275397
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegion

 

_**Última modificación del tema:** 2015-03-09_

Recupera una o varias regiones de red. Las regiones de red representan concentradores o redes troncales de red en una red de empresa. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

El Ejemplo 1 recupera todas las regiones de red de la organización.

    Get-CsNetworkRegion

## EJEMPLO 2

El Ejemplo 2 recupera las regiones de red con la Identity Norteamérica. Debido a que las identidades son únicas, este comando recupera al máximo una región de red.

    Get-CsNetworkRegion -Identity NorthAmerica

## EJEMPLO 3

Este ejemplo recupera todas las regiones de red con identidades que finalizan con la cadena de caracteres "America". Esto recuperaría regiones con identidades como Norteamérica, Sudamérica y América Central.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## EJEMPLO 4

En este ejemplo se recuperan todas las regiones de red asociadas con el sitio central Redmond. En primer lugar, el comando llama al cmdlet **Get-CsNetworkRegion** sin parámetros, para recuperar una colección con todas las regiones de red que se han definido para la implementación de Lync Server. A continuación, esta colección se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** filtra esta colección para devolver solo aquellos elementos (regiones de red) cuyo valor de CentralSite es igual a (-eq) site:Redmond.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## Descripción detallada

Una región de red interconecta diversas partes de una red a través de diversas áreas geográficas. Cada región de red debe asociarse con un sitio central. Use este cmdlet para recuperar información acerca de una o más regiones de red, incluido el sitio central asociado y las opciones que determinan si están permitidas las rutas de acceso alternativas para las conexiones de audio y vídeo, y que asocian los sitios de la región con una configuración de omisión de medios.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Get-CsNetworkRegion** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegion"}

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
<td><p>Este parámetro permite realizar una búsqueda de caracteres comodín en la Identity de todas las regiones de red configuradas para la organización. Use el carácter comodín para filtrar en alguna parte de la Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador único de la región de contacto que se quiere recuperar. La Identity será en forma de una cadena que identifica exclusivamente esa región. (Observe que la Identity es lo mismo que NetworkRegionID).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información de la región de red desde una réplica local de Almacén de administración central, en lugar de Almacén de administración central en sí.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Recupera uno o más objetos del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vea también

#### Otros recursos

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

