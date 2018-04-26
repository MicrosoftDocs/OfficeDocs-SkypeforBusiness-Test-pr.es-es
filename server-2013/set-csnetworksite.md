---
title: Set-CsNetworkSite
TOCTitle: Set-CsNetworkSite
ms:assetid: 221a099c-72c4-4eb0-8812-6b2b7639a9ee
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398295(v=OCS.15)
ms:contentKeyID: 48274643
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSite

 

_**Última modificación del tema:** 2015-03-09_

Modifica un sitio de red existente definido para un control de admisión de llamadas (CAC) o 9-1-1 mejorado (E9-1-1). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSite [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-LocationPolicy <String>] [-NetworkRegionID <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se modifica el sitio de red denominado Vancouver. El nombre de sitio que se está modificando se especifica como el valor de parámetro Identity. El sitio Vancouver se mueve a una nueva región, lo que requiere que se cambie el parámetro NetworkRegionID, en este caso a la región denominada Canada. Como se ha suministrado un NetworkRegionID, pero no se ha especificado ningún valor para BypassID, este se generará automáticamente. Cualquier Id. de desvío existente se sobrescribirá.

    Set-CsNetworkSite -Identity Vancouver -NetworkRegionID Canada

## EJEMPLO 2

En el ejemplo 2, simplemente se modifica el perfil de directivas de banda ancha asociado al sitio Vancouver. El nombre de sitio se especifica como el valor de parámetro Identity. A continuación, se especifica un valor para el parámetro BWPolicyProfileID: LowBWLimits. Se usarán para este sitio las directivas asociadas a ese perfil.

    Set-CsNetworkSite -Identity Vancouver - BWPolicyProfileID LowBWLimits

## Descripción detallada

Los sitios de red son las oficinas o ubicaciones configuradas dentro de cada región de una implementación de E9-1-1 o CAC. Este cmdlet modifica la configuración de un sitio existente. Esto puede incluir la región a la que está asociado el sitio, la descripción del sitio y el perfil de directivas de banda ancha asociado.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsNetworkSite** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSite"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La Identidad del perfil de directiva de ancho de banda que definirá las limitaciones de este sitio. Puede recuperar una lista de los perfiles disponibles llamando al cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p>
<p>Si especifica un valor para este parámetro, debe especificar también un valor para el parámetro NetworkRegionID.</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Un identificador único global (GUID). Este GUID se usará para asignar sitios de red a valores de desviación de medios en una configuración de red CAC o E9-1-1. (Use este valor de BypassID en la llamada al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>).</p>
<p>Si especifica un valor para este parámetro, debe especificar también un valor para el parámetro NetworkRegionID. Si no especifica un valor para este parámetro, pero especifica uno para NetworkRegionID, se generará automáticamente un BypassID.</p>
<p>Si especifica un valor de forma explícita, debe tener el formato de un GUID (por ejemplo, 3b24a047-dce6-48b2-9f20-9fbff17ed62a). Le recomendamos que suministre un valor para NetworkRegionID y permita que el valor de BypassID se genere automáticamente. Si escribe manualmente un valor, recibirá una pregunta de confirmación para indicar que no desea generar el valor automáticamente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Una cadena que describe el sitio. Este parámetro se puede usar para ofrecer una explicación más descriptiva de la naturaleza o ubicación del sitio, lo que no puede expresarse en la Identidad.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Cuando se establece en True, el enrutamiento de voz se administrará teniendo en cuenta la ubicación tanto del usuario que realiza la llamada como del usuario que la recibe. El valor predeterminado es False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>El identificador único del sitio de red que se quiere modificar. Los sitios se crean únicamente en el ámbito global, de modo que no es necesario especificar el ámbito. En su lugar, se debe especificar únicamente el Id. del sitio de red.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>DisplayNetworkSiteType</p></td>
<td><p>Una referencia a un objeto de sitio de red (un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType). Este objeto puede recuperarse llamando al cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>El nombre de la directiva de ubicación asociada a este sitio. La directiva de ubicación asigna valores específicos de E9-1-1 al sitio. Para obtener una lista de las directivas de ubicación, llame al cmdlet <strong>Get-CsLocationPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La Identidad de la región de la red a la que está asociado este sitio. Este parámetro debe contener un valor si desea facilitar un BypassID (ya sea por autogeneración o manualmente) o si la propiedad EnableBandwidthPolicyCheck de la configuración de red es True. Para recuperar las opciones de configuración de red, llame al cmdlet <strong>Get-CsNetworkConfiguration</strong>.</p>
<p>Si ya existe un BypassID en este sitio y no se especifica un valor para el parámetro BypassID, un BypassID generado automáticamente sobrescribirá el BypassID existente.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La directiva de enrutamiento de voz por usuario que se asignará al sitio. Por ejemplo:</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>Tenga en cuenta que debe especificar una directiva por usuario, ya que no se pueden asignar directivas de sitio o globales a un sitio con el parámetro VoiceRoutingPolicy.</p>
<p>Este parámetro se introdujo en la versión de febrero de 2013 de Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType. Acepta entradas canalizadas de objetos de sitio de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vea también

#### Otros recursos

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

