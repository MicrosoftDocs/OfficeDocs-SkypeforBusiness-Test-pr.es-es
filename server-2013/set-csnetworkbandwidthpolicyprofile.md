---
title: Set-CsNetworkBandwidthPolicyProfile
TOCTitle: Set-CsNetworkBandwidthPolicyProfile
ms:assetid: 519916b9-d5a0-476e-a516-9b8a3058daf2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398338(v=OCS.15)
ms:contentKeyID: 48275226
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkBandwidthPolicyProfile

 

_**Última modificación del tema:** 2015-03-09_

Modifica un perfil de directiva de ancho de banda de red existente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkBandwidthPolicyProfile [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo se modifica la descripción del perfil de directiva de ancho de banda con el valor de Identity de LowBWProfile. Para ello, se llama al cmdlet **Set-CsNetworkBandwidthPolicyProfile** con dos parámetros: Identity (que especifica el nombre del perfil que se debe modificar) y Description (que especifica la nueva descripción del perfil).

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -Description "Policy for links of less than 10MB"

## EJEMPLO 2

En el ejemplo 2 se modifica el límite general y el límite de las sesiones de transmisión de vídeo para el perfil de la directiva de ancho de banda con Identidad LowBWLimit. Después de especificar el valor de Identity del perfil que se va a cambiar, usamos a continuación el parámetro VideoBWLimit para establecer el límite general de vídeo en 2500. Después, usamos el parámetro VideoBWSessionLimit para establecer el límite de sesión individual en 300. Este comando agregará un perfil de vídeo o actualizará uno existente para el perfil de la directiva de ancho de banda LowBWLimit. Los perfiles existentes de audio no se verán afectados.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -VideoBWLimit 2500 -VideoBWSessionLimit 300

## EJEMPLO 3

En este ejemplo se crea una nueva directiva de ancho de banda y se asigna al perfil correspondiente con el valor de Identity de LowBWLimit. La primera línea de este ejemplo es una llamada al cmdlet **New-CsNetworkBWPolicy**, que crea un nuevo perfil. En este caso, un perfil de vídeo (-BWPolicyModality video) con un límite de 5.000 kbps (-BWLimit 5000) y un límite de sesión de 200 kbps (-BWSessionLimit 200). Este nuevo objeto de perfil se almacena en la variable $bp. La siguiente línea del ejemplo llama al cmdlet **Set-CsNetworkBandwidthPolicyProfile** para modificar el perfil LowBWLimit (-Identity LowBWLimit). El parámetro BWPolicy se usa con un valor de $bp, lo que reemplaza cualquier directiva existente de este perfil por la directiva que se acaba de crear y se encuentra almacenada en la variable $bp.

    $bp = New-CsNetworkBWPolicy -BWLimit 5000 -BWSessionLimit 200 -BWPolicyModality video
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bp

## EJEMPLO 4

En el ejemplo 4 se agrega una nueva directiva de ancho de banda de audio al conjunto de directivas existentes del perfil LowBWProfile. En la línea 1 se llama al cmdlet **Get-CsNetworkBandwidthPolicyProfile** para recuperar el perfil con el valor de Identity de LowBWProfile. Dicho perfil se almacena en la variable $a. En la siguiente línea, se llama al cmdlet **New-CsNetworkBWPolicy** para crear una nueva directiva de ancho de banda. Se trata de una directiva de audio (-BWPolicyModality audio), con un límite de 2.000 kbps (-BWLimit 2000) y un límite de sesión de 300 kbps (-BWSessionLimit 300). Esta nueva directiva se almacena en la variable $ap.

En la línea 3, se agrega la nueva directiva de audio (almacenada en $ap) al perfil recuperado en la línea 1 (y almacenado en la variable $a). Esto se hace abriendo el método Agregar de la propiedad BWPolicy del perfil, pasando un valor de $ap. Esto puede leerse como "Agregar la nueva directiva almacenada en $ap a BWPolicy del perfil LowBWProfile (almacenado en $a)".

Por último, se llama al cmdlet **Set-CsNetworkBandwidthPolicyProfile** para actualizar el perfil LowBWProfile y se usa el parámetro Instance con un valor de $a, que contiene el perfil modificado.

    $a = Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile
    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    $a.BWPolicy.Add($ap)
    Set-CsNetworkBandwidthPolicyProfile -Instance $a

## EJEMPLO 5

El Ejemplo 5 es idéntico en funcionalidad al Ejemplo 4: agrega una nueva directiva de audio a la lista existente de directivas para el perfil LowBWProfile. Este método necesita de menos líneas, pero puede no ser tan claro. Lo hemos incluido para demostrar que hay formas diferentes de hacer lo mismo.

En la línea 1 se crea una nueva directiva de ancho de banda de audio, con límites de ancho de banda (2.000) y de sesión (300), que almacena el nuevo objeto en la variable $ap. A continuación, se llama al cmdlet **Set-CsNetworkBandwidthPolicyProfile** para modificar el perfil con el valor de Identity de LowBWProfile. Con el parámetro BWPolicy se modifica la lista de directivas del perfil. Observe el valor que se ha transferido para este parámetro: @{add=$ap}. De este modo, Windows PowerShell puede agregar elementos a una lista. Comienza con el símbolo @, seguido de un conjunto de llaves {} que contienen la acción especificada que se desea realizar en la lista (en este caso queremos agregar a la lista, aunque también se puede eliminar o reemplazar). Tas la acción (agregar) se incluye un signo igual, seguido del objeto que deseamos agregar a la lista (en este caso, la nueva directiva que se encuentra almacenada en la variable $ap).

    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -BWPolicy @{add=$ap}

## Descripción detallada

Como parte del control de admisión de llamadas (CAC), se usa una directiva de ancho de banda para definir las limitaciones de ancho de banda de ciertas modalidades. (En Lync Server solo se pueden asignar limitaciones de ancho de banda a las modalidades de audio y vídeo). Este cmdlet modifica un perfil de contenedor para estas directivas.

IMPORTANTE: Si un perfil contiene múltiples directivas (por ejemplo, una directiva de audio y otra de vídeo), al modificar el perfil usando las propiedades de AudioBWLimit, AudioBWSessionLimit, VideoBWLimit o VideoBWSessionLimit se eliminarán todas las directivas existentes en el perfil y se sustituirán con los nuevos valores. Si el perfil incluía una directiva para limitar el vídeo y solo configura el parámetro AudioBWLimit, la directiva de vídeo se eliminará y se creará una directiva de audio.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsNetworkBandwidthPolicyProfile** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a todas las conexiones de audio. Si una sola sesión de audio provoca que se exceda el límite de ancho de banda de audio, no se permitirá que dicha sesión se inicie.</p>
<p>Expresado en kbps. Por ejemplo, un valor de 1000 significaría 1000 kbps.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: Si facilita un valor para el parámetro AudioBWSessionLimit, pero no para AudioBWLimit, AudioBWLimit se establecerá de forma predeterminada en 0.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a cada conexión de audio. Expresado en kbps. El valor debe ser mayor o igual que 40.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: Si facilita un valor para el parámetro AudioBWLimit, pero no para AudioBWSessionLimit, AudioBWSessionLimit se establecerá de forma predeterminada en 175.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de objetos que contienen perfiles de directiva de ancho de banda. Cada objeto de la lista consta de una modalidad de ancho de banda (audio o vídeo), una limitación de ancho de banda y una limitación de sesión de ancho de banda.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor a los parámetros AudioBWLimit, AudioBWSessionLimit, VideoBWLimit ni VideoBWSessionLimit.</p>
<p>Los objetos de la lista deben ser del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType. Los objetos de este tipo se pueden crear llamando al cmdlet <strong>New-CsNetworkBWPolicy</strong> y la directiva resultante se puede agregar al perfil asignándola como valor a este parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Una descripción del perfil de directiva de ancho de banda. Por ejemplo, puede usar este parámetro para describir el uso para el que se ha diseñado el perfil.</p></td>
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
<td><p>El valor de cadena que identifica de manera unívoca el perfil de directiva de ancho de banda que desea modificar. Es idéntico a la propiedad BWPolicyProfileID del perfil y puede cambiarse mediante el cambio del valor de dicha propiedad. Esta operación es equivalente a &quot;cortar y pegar&quot;: todas las propiedades del perfil serán las mismas y solo cambiará el nombre. Sin embargo, este valor no puede cambiarse si el perfil se asigna a un sitio de red.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>BWPolicyProfileType</p></td>
<td><p>Una referencia a un objeto de perfil de directiva de ancho de banda (un objeto del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType) que contiene la configuración que se desea usar para modificar el perfil. Este objeto se puede recuperar llamando al cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a todas las conexiones de vídeo. Si una sola sesión de vídeo provoca que se exceda el límite de ancho de banda de vídeo, no se permitirá que dicha sesión inicie.</p>
<p>Expresado en kbps. Por ejemplo, un valor de 1000 significaría 1000 kbps.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: Si facilita un valor para el parámetro VideoBWSessionLimit, pero no para VideoBWLimit, VideoBWLimit se establecerá de forma predeterminada en 0.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La cantidad máxima de ancho de banda que se puede asignar a cada conexión de vídeo. Expresado en kbps. El valor debe ser mayor o igual que 100.</p>
<p>Si facilita un valor para este parámetro, no puede facilitar ningún valor al parámetro BWPolicy.</p>
<p>Valor predeterminado: Si facilita un valor para el parámetro VideoBWLimit, pero no para VideoBWSessionLimit, VideoBWSessionLimit se establecerá de forma predeterminada en 700.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType. Acepta entradas canalizadas de objetos de perfil de directiva de ancho de banda de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Modifica un objeto del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vea también

#### Otros recursos

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

