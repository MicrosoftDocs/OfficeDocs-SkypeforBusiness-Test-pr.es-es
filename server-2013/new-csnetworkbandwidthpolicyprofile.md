---
title: New-CsNetworkBandwidthPolicyProfile
TOCTitle: New-CsNetworkBandwidthPolicyProfile
ms:assetid: 84940891-37a6-45fc-972d-05b95aa71ba9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398675(v=OCS.15)
ms:contentKeyID: 48275895
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBandwidthPolicyProfile

 

_**Última modificación del tema:** 2015-03-09_

Crea un nuevo perfil de directiva de ancho de banda para la red. También se puede usar para establecer las directivas de ancho de banda del perfil. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En el ejemplo 1 se crea un nuevo perfil de directiva de ancho de banda llamado LowBWLimits. Este nuevo perfil tendrá dos directivas asignadas, una de audio y otra de vídeo (las dos únicas posibles en Lync Server). Para agregar al perfil la directiva de audio, se usa el parámetro AudioBWLimit para asignar un límite de 2000 kbps (en este caso) a todas las conexiones de audio, y el parámetro AudioBWSessionLimit para asignar un límite de 200 kbps a las sesiones de audio individuales. Para crear límites de sesiones de vídeo, se lleva a cabo el mismo proceso, pero con los parámetros VideoBWLimit y VideoBWSessionLimit.

    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimits -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400 -VideoBWSessionLimit 500

## Descripción detallada

Como parte del control de admisión de llamadas (CAC), se usa una directiva de ancho de banda para definir las limitaciones de ancho de banda de ciertas modalidades. (En Lync Server, solo se pueden asignar limitaciones de ancho de banda a las modalidades de audio y vídeo). Este cmdlet crea un perfil de contenedor para estas directivas. Al llamar a este cmdlet, defina las directivas individuales dentro del contenedor especificando las limitaciones de ancho de banda para audio y vídeo.

Para aplicar perfiles de directiva de ancho de banda a los sitios de red, es necesario llamar a los cmdlet **New-CsNetworkSite** o **Set-CsNetworkSite**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **New-CsNetworkBandwidthPolicyProfile** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Un valor alfanumérico que identifica la directiva de forma única. Todos los perfiles de directiva de ancho de banda se crean en el ámbito global. Por ello, el ámbito está implícito y solo es necesario especificar un nombre único al crear un nuevo perfil de directiva de ancho de banda. Tenga en cuenta que este valor rellena también la propiedad BWPolicyProfileID del perfil.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a todas las conexiones de audio. Si una sola sesión de audio provoca que se exceda el límite de ancho de banda de audio, no se permitirá que dicha sesión se inicie.</p>
<p>Expresado en kbps. Por ejemplo, un valor de 1000 significaría 1000 kbps.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: si proporciona un valor al parámetro AudioBWSessionLimit, pero no a AudioBWLimit, AudioBWLimit se establece en 0 de manera predeterminada.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a cada conexión de audio. Expresado en kbps. El valor debe ser mayor o igual que 40.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: si proporciona un valor al parámetro AudioBWLimit, pero no a AudioBWSessionLimit, AudioBWSessionLimit se establece en 175 de manera predeterminada.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Una lista de objetos que contienen perfiles de directiva de ancho de banda. Cada objeto de la lista consta de una modalidad de ancho de banda (audio o vídeo), una limitación de ancho de banda y una limitación de sesión de ancho de banda.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor a los parámetros AudioBWLimit, AudioBWSessionLimit, VideoBWLimit ni VideoBWSessionLimit.</p>
<p>Los objetos de la lista se pueden crear llamando al cmdlet <strong>New-CsNetworkBWPolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Una descripción del perfil de directiva de ancho de banda. Por ejemplo, puede usar este parámetro para describir el uso para el que se ha diseñado el perfil.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecen antes de hacer cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a todas las conexiones de vídeo. Si una sola sesión de vídeo provoca que se exceda el límite de ancho de banda de vídeo, no se permitirá que dicha sesión inicie.</p>
<p>Expresado en kbps. Por ejemplo, un valor de 1000 significaría 1000 kbps.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: si proporciona un valor al parámetro VideoBWSessionLimit, pero no a VideoBWLimit, VideoBWLimit se establece en 0 de manera predeterminada.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a cada conexión de vídeo. Expresado en kbps. El valor debe ser mayor o igual que 100.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: Si proporciona un valor al parámetro VideoBWLimit, pero no a VideoBWSessionLimit, VideoBWSessionLimit se establece en 700 de manera predeterminada.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Crea un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vea también

#### Otros recursos

[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

