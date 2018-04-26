---
title: Get-CsNetworkConfiguration
TOCTitle: Get-CsNetworkConfiguration
ms:assetid: 08bc8eca-b244-4d5e-b089-1cc95605ba14
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398140(v=OCS.15)
ms:contentKeyID: 48274356
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Recupera la configuración global del control de admisión de llamadas (CAC), E9-1-1 mejorado (E9-1-1) y omisión de medios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se recupera la configuración de red. Esta configuración se define únicamente en el ámbito global, por lo que solo se devolverá un elemento.

    Get-CsNetworkConfiguration

## EJEMPLO 2

Solo existe un conjunto de configuraciones de omisión de medios que se aplica globalmente. Este conjunto se encuentra almacenado como parte de la configuración de red general. Este comando recupera primero dicha configuración al llamar al cmdlet **Get-CsNetworkConfiguration** y luego recupera la propiedad MediaBypassSettings de la configuración.

    (Get-CsNetworkConfiguration).MediaBypassSettings

## Descripción detallada

El objeto de configuración de red contiene todas las configuraciones globales de la omisión de medios y de una configuración CAC completa en una implementación de Lync Server, por ejemplo, si esta última configuración se habilitó o no. Puede usar este cmdlet para recuperar dichas configuraciones. No obstante, a fin de recuperar la configuración CAC, se recomienda el uso de cmdlets específicos del tipo de objeto, a excepción de EnableBandwidthPolicyCheck y MediaBypassSettings. Por ejemplo, para recuperar las regiones de red normalmente resulta más fácil llamar al cmdlet **Get-CsNetworkRegion** que al cmdlet **Get-CsNetworkConfiguration** y después recuperar la propiedad NetworkRegions de esa configuración.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Get-CsNetworkConfiguration** en forma local: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkConfiguration"}

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
<td><p>Dado que solo habrá una configuración red en todo momento, este parámetro no es necesario con este cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Siempre será Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información de configuración de red de la réplica local de Almacén de administración central, en lugar del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Get-CsNetworkConfiguration** devuelve una instancia del objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Vea también

#### Otros recursos

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

