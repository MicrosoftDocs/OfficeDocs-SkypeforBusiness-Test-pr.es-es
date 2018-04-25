---
title: Get-CsNetworkBandwidthPolicyProfile
TOCTitle: Get-CsNetworkBandwidthPolicyProfile
ms:assetid: 31784852-0cf4-4114-bf92-5eef6f346c47
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425815(v=OCS.15)
ms:contentKeyID: 48274860
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkBandwidthPolicyProfile

 

_**Última modificación del tema:** 2015-03-09_

Recupera uno o más perfiles de directivas de ancho de banda de red. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkBandwidthPolicyProfile [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

Si se llama al cmdlet **Get-CsNetworkBandwidthPolicyProfile** sin ningún parámetro, se recuperarán todos los perfiles de directiva de ancho de banda definidos en la implementación de Lync Server.

    Get-CsNetworkBandwidthPolicyProfile

## EJEMPLO 2

En este ejemplo se recupera el perfil de las directivas de ancho de banda con Identity LowBWProfile. Como las identidades deben ser únicas, esto devolverá un perfil como máximo.

    Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## EJEMPLO 3

En este ejemplo se utiliza el parámetro Filter para especificar uno o más perfiles para recuperar según una cadena de caracteres comodín. Hemos utilizado la cadena \*50MB\*, que indica que deseamos recuperar todos los perfiles de directivas de ancho de banda con valores Identity que contengan la cadena 50MB en cualquier posición. Por ejemplo, esto recuperaría perfiles con identidades como "BW profile for 50MB links", "50MB audio limit" y "video limits of 50MB".

    Get-CsNetworkBandwidthPolicyProfile -Filter *50MB*

## Descripción detallada

Como parte del control de admisión de llamadas (CAC), se usa una directiva de ancho de banda para definir las limitaciones de ancho de banda de ciertas modalidades. (En Lync Server solo se pueden asignar limitaciones de ancho de banda a las modalidades de audio y vídeo.) Este cmdlet recupera uno más perfiles de contenedor para esas directivas.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Get-CsNetworkBandwidthPolicyProfile** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Una cadena que contiene caracteres comodín utilizada para recuperar perfiles de directivas de ancho de banda que tienen valores Identity que coinciden con el patrón de comodín.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Un valor de cadena que únicamente identifica el perfil de las directivas de ancho de banda que desea recuperar. Si se especifica una Identidad, se recuperará un perfil como máximo.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera el perfil de directiva de ancho de banda de red a partir de una réplica local de Almacén de administración central en lugar de hacerlo directamente desde Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vea también

#### Otros recursos

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

