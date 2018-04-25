---
title: Get-CsNetworkSite
TOCTitle: Get-CsNetworkSite
ms:assetid: 9627869d-101f-4668-bee2-01fce1d84cbd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398766(v=OCS.15)
ms:contentKeyID: 48276080
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSite

 

_**Última modificación del tema:** 2015-03-09_

Recupera uno o más sitios de red definidos para el control de admisión de llamadas (CAC) o 9-1-1 mejorado (E9-1-1). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

Al llamar al cmdlet **Get-CsNetworkSite** sin ningún parámetro, se devuelven todos los sitios de red configurados para CAC o E9-1-1 dentro de la implementación de Lync Server.

    Get-CsNetworkSite

## Ejemplo 2

Este comando recupera el sitio con la identidad (y, por definición, el NetworkSiteID) Redmond.

    Get-CsNetworkSite -Identity Redmond

## Ejemplo 3

El comando del ejemplo 3 llama al cmdlet **Get-CsNetworkSite** con el parámetro Filter. El valor de parámetro Filter es NA\*, de modo que este comando recuperará todos los sitios cuya identidad comience con la cadena NA seguida de cualquier cantidad de caracteres. Esta acción recuperará sitios como NARedmond, NAVancouver y NAChicago.

    Get-CsNetworkSite -Filter NA*

## Ejemplo 4

En el ejemplo 4 se usan dos cmdlets, **Get-CsNetworkSite** y **Where-Object**, para recuperar todos los sitios que forman parte de la región NorthAmerica. El comando empieza por llamar al cmdlet **Get-CsNetworkSite** sin ningún parámetro para recuperar todos los sitios de red. Después, la colección de sitios se canaliza al cmdlet **Where-Object**, que filtra la colección en busca de todos los sitios cuya propiedad NetworkRegionID sea igual a (-eq) NorthAmerica.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"}

## Descripción detallada

Los sitios de red son las oficinas o ubicaciones configuradas dentro de cada región de una implementación de CAC o E9-1-1. Este cmdlet recupera las configuraciones de uno o más sitios existentes.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Get-CsNetworkSite** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSite"}

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
<td><p>Una cadena comodín que permite recuperar varios sitios según la coincidencia entre la identidad del sitio y el valor de Filter.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>El identificador único del sitio de red que se quiere recuperar. Los sitios se crean únicamente en el ámbito global, de modo que no es necesario especificar el ámbito. Solo deberá especificar el Id. de sitio (el valor de este Id. coincide con el NetworkSiteID del sitio de red).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información del sitio de red de la réplica local de Almacén de administración central en lugar de hacerlo directamente de Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Recupera un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vea también

#### Otros recursos

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

