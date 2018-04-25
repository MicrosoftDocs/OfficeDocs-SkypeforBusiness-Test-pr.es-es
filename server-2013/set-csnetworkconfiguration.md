---
title: Set-CsNetworkConfiguration
TOCTitle: Set-CsNetworkConfiguration
ms:assetid: d54dc154-c092-4be9-8656-f7fec3fbd835
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398927(v=OCS.15)
ms:contentKeyID: 48276799
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica los parámetros de una configuración de red. Este cmdlet normalmente se usará para habilitar o deshabilitar el control de admisión de llamadas (CAC) Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfiles <PSListModifier>] [-Confirm [<SwitchParameter>]] [-EnableBandwidthPolicyCheck <$true | $false>] [-Force <SwitchParameter>] [-InterNetworkRegionRoutes <PSListModifier>] [-InterNetworkSitePolicies <PSListModifier>] [-MediaBypassSettings <MediaBypassSettingsType>] [-NetworkRegionLinks <PSListModifier>] [-NetworkRegions <PSListModifier>] [-NetworkSites <PSListModifier>] [-Subnets <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando de este ejemplo ejecutará una comprobación de validación en toda la configuración de CAC y, a continuación, (según cuáles sean sus respuestas a las advertencias devueltas) habilitará el CAC. Si el CAC ya está habilitado (en otras palabras, si la propiedad EnableBandwidthPolicyCheck está definida en True) y ejecuta este comando, simplemente se ejecutará la comprobación de validación.

    Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck $True

## Descripción detallada

El objeto de configuración de red contiene todos los parámetros de una configuración de CAC completa en una implementación de Lync Server, además de la configuración de omisión de medios. Puede usar este cmdlet para modificar cualquier parte de la configuración del CAC y deberá usarlo si necesita cambiar la configuración de omisión de medios. Sin embargo, es recomendable que use cmdlets específicos del tipo de objeto para modificar la mayoría de opciones de configuración del CAC. Por ejemplo, para trabajar con regiones de red, use los cmdlets que acaben con el nombre CsNetworkRegion, en lugar de manipular el parámetro NetworkRegions de este cmdlet.

El uso principal de este cmdlet es habilitar y deshabilitar el CAC, así como aplicar la configuración de omisión de medios. Una vez definidos los distintos componentes necesarios para la configuración (como son las regiones, los sitios y las subredes), debe habilitar la configuración para que funcione. Para ello, defina el parámetro EnableBandwidthPolicyCheck en True. Tenga en cuenta que al ejecutar este cmdlet con el parámetro EnableBandwidthPolicyCheck definido en True, no se habilita el CAC de inmediato. Antes de poder habilitarlo, se lleva a cabo una serie de comprobaciones de validación para garantizar que la configuración esté definida correctamente. Los errores o discrepancias en la configuración se notificarán con advertencias, donde se le preguntará si desea continuar para habilitar el CAC aunque haya un problema. Si decide continuar (pulsando Entrar o Y), la validación continuará y, si se detectan nuevos problemas, se le volverá a notificar.

Si completa la validación, si se opta por continuar en todas las advertencias, EnableBandwidthPolicyCheck se establecerá en True y el CAC se habilitará, pero hasta que no se hayan resuelto los problemas, es probable que no funcione de la forma esperada. Si en algún momento decide detener la validación (escribiendo N en una advertencia), la validación finalizará y el valor de EnableBandwidthPolicyCheck continuará siendo False (el valor predeterminado).

Si el parámetro EnableBandwidthPolicyCheck ya está establecido en True, puede llamar al cmdlet **Set-CsNetworkConfiguration** y enviar un valor de True al parámetro EnableBandwidthPolicyCheck para ejecutar la validación sin modificar la configuración. Asimismo, cuando el valor de EnableBandwidthPolicyCheck sea True, todos los cambios que intente realizar llamando al cmdlet **Set-CsNetworkConfiguration** volverán a hacer que se ejecute la comprobación de validación.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Set-CsNetworkConfiguration**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkConfiguration"}

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
<td><p><em>BWPolicyProfiles</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una recopilación de todos los perfiles de directiva de ancho de banda que se pueden asignar a sitios, directivas entre sitios o vínculos de regiones de red. Todos los perfiles de directiva de ancho de banda contienen limitaciones de ancho de banda (limitaciones generales y limitaciones de sesiones) para las conexiones de vídeo y audio. Mediante una llamada al cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong> se puede recuperar una lista completa de perfiles de directiva de ancho de banda.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBandwidthPolicyCheck</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Si se define este parámetro en True, se ejecutará una comprobación de validación en toda la configuración de CAC. Si se superan todas las comprobaciones de validación o si decide omitir todas las advertencias, el CAC se habilitará. Si no se supera alguna de las comprobaciones de validación, puede detener la validación y el valor de EnableBandwidthPolicyCheck no cambiará. Antes de realizar la comprobación de validación, asegúrese de definir rutas de región entre cada par de regiones de red.</p>
<p>Si este valor se define en False, el CAC se deshabilitará.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Este parámetro no admite ningún valor. Si incluye este parámetro, cualquier cambio aplicado a la configuración, incluida la habilitación de la configuración, se llevará a cabo sin advertencias ni comprobaciones de validación.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Este valor siempre será Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>NetworkConfigurationSettings</p></td>
<td><p>Una referencia a un objeto de configuración de red. Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings y puede recuperarse mediante una llamada al cmdlet <strong>Get-CsNetworkConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InterNetworkRegionRoutes</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una recopilación de todas las rutas de regiones de red definidas en la configuración de CAC. Para recuperar todos los miembros de la colección, llame al cmdlet <strong>Get-CsNetworkInterRegionRoute</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicies</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una colección de todas las directivas entre sitios de red definidas en la configuración de CAC. Para recuperar todos los miembros de la colección, llame al cmdlet <strong>Get-CsNetworkInterSitePolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaBypassSettings</em></p></td>
<td><p>Opcional</p></td>
<td><p>MediaBypassSettingsType</p></td>
<td><p>Una referencia a un objeto que define la configuración global de omisión de medios para la configuración de CAC. Al definir este valor, se sobrescribe la configuración de omisión de medios existente. Para obtener esta referencia a objeto, llame al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong> y asigne las nuevas opciones de configuración a una variable. Envíe esta variable al parámetro MediaBypassSettings para cambiar la configuración global de omisión de medios.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una recopilación de todos los vínculos de regiones de red definidos en la configuración de CAC. Cada vínculo de región de red define una conexión que existe entre dos regiones y cualquier limitación de ancho de banda que se deba aplicar a las conexiones entre dichas regiones. Para recuperar todos los miembros de la colección, llame al cmdlet <strong>Get-CsNetworkRegionLink</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegions</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una recopilación de regiones de red (cada una de las cuales representa un concentrador o una red troncal dentro de la red) definidas en la configuración de CAC. Para recuperar todos los miembros de la colección, llame al cmdlet <strong>Get-CsNetworkRegion</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSites</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una recopilación de sitios de red (cada uno de los cuales representa una oficina o ubicación dentro de una red) definidos en la configuración de CAC. Para recuperar todos los miembros de la colección, llame al cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnets</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una colección de subredes de la red (cada una de las cuales asocia un extremo con un sitio) definidas en la configuración de CAC. Para recuperar todos los miembros de la colección, llame al cmdlet <strong>Get-CsNetworkSubnet</strong>.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings. Acepta entradas canalizadas de un objeto de configuración de red.

## Tipos de valores devueltos

El cmdlet **Set-CsNetworkConfiguration** no devuelve ningún valor u objeto. En su lugar, el cmdlet modifica instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Vea también

#### Otros recursos

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)

