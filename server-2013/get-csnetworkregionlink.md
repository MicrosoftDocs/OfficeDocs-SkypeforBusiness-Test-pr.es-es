---
title: Get-CsNetworkRegionLink
TOCTitle: Get-CsNetworkRegionLink
ms:assetid: dc5cb988-13e2-4af4-8b36-0aaa58ebf1c5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398972(v=OCS.15)
ms:contentKeyID: 48276905
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegionLink

 

_**Última modificación del tema:** 2015-03-09_

Recupera uno o más vínculos entre las regiones de red configuradas para el control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegionLink [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

En el ejemplo 1 se recuperan todos los vínculos de región de red definidos en una implementación de Lync Server.

    Get-CsNetworkRegionLink

## Ejemplo 2

En el ejemplo 2 se recupera información sobre un vínculo de región de red (como máximo), el vínculo con la identidad NA\_EMEA.

    Get-CsNetworkRegionLink -Identity NA_EMEA

## Ejemplo 3

En este ejemplo se usa el parámetro Filter para recuperar todos los vínculos de región de red cuyo nombre (identidad) de vínculo contenga la cadena EMEA. Observe los caracteres \*, uno delante de la cadena EMEA y otro detrás. Esto significa que la cadena puede estar precedida o seguida de uno o varios caracteres; la cadena EMEA simplemente debe incluirse en alguna parte de Identity. Se recuperarán los vínculos con nombres como NA\_EMEA, EMEA\_APAC y EMEA2\_SA.

    Get-CsNetworkRegionLink -Filter *EMEA*

## Ejemplo 4

En este ejemplo se recuperan todos los vínculos de región de red que incluyen EMEA como una de las dos regiones que se vinculan. El ejemplo empieza con una llamada al cmdlet **Get-CsNetworkRegionLink** sin parámetros, con lo cual se recuperan todos los vínculos de región. Esta colección de vínculos se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** examina cada miembro de la colección de forma individual y comprueba los valores de las propiedades NetworkRegionID1 y NetworkRegionID2. Si alguna de estas propiedades es igual a EMEA, o, lo que es lo mismo, si NetworkRegionID1 es igual a (-eq) EMEA o (-or) NetworkRegionID2 es igual a (-eq) EMEA, se conserva el elemento en la colección y se muestra.

    Get-CsNetworkRegionLink | Where-Object {$_.NetworkRegionID1 -eq "EMEA" -or $_.NetworkRegionID2 -eq "EMEA"}

## Descripción detallada

Las regiones de una red se vinculan a través de conectividad WAN física. Este cmdlet recupera uno o más vínculos de región definidos en las opciones de configuración de red para una implementación de Lync Server.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Get-CsNetworkRegionLink**: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegionLink"}

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
<td><p>Acepta una cadena de caracteres comodín que se usa para recuperar vínculos de red basados en la coincidencia del valor de Identity con la cadena de caracteres comodín.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador único del vínculo de región de red que se quiere recuperar. Los vínculos de región de red se crean solo en el ámbito global, de modo que este identificador no necesita especificar ningún ámbito. En lugar de ello, contiene una cadena que es un nombre único que identifica el vínculo. (Tenga en cuenta que este valor es el mismo que NetworkRegionLinkID.)</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información del vínculo de región de red de la réplica local del Almacén de administración central, en lugar de recuperarla del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Recupera uno o más objetos del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vea también

#### Otros recursos

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

