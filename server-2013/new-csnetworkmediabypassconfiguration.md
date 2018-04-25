---
title: New-CsNetworkMediaBypassConfiguration
TOCTitle: New-CsNetworkMediaBypassConfiguration
ms:assetid: 24055ae5-7fc8-4ca5-9e65-ac3a1f17b405
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425718(v=OCS.15)
ms:contentKeyID: 48274678
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkMediaBypassConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea una nueva configuración global para la desviación de medios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsNetworkMediaBypassConfiguration [-AlwaysBypass <$true | $false>] [-BypassID <String>] [-Enabled <$true | $false>] [-EnableDefaultBypassID <$true | $false>] [-EnabledForAudioVideoConferences <$true | $false>] [-ExternalBypassMode <Off | ICE | Any>] [-InternalBypassMode <Off | ICE | Any>]

## Ejemplos

## EJEMPLO 1

Los comandos de este ejemplo habilitan la desviación de medios y la configuran para intentar siempre el desvío. La primera línea del ejemplo es una llamada al cmdlet **New-CsNetworkMediaBypassConfiguration**. Se pasan dos parámetros a este cmdlet: AlwaysBypass y Enabled, establecidos los dos en True ($true). Al establecer Enabled en True, se habilita la desviación de medios, mientras que al establecer AlwaysBypass en True, se garantiza que se intentará realizar la desviación de medios en todas las llamadas. (Tenga en cuenta que al configurar estos dos parámetros se generará automáticamente un valor para la propiedad BypassID). El cmdlet **New-CsNetworkMediaBypassConfiguration** crea el objeto únicamente en la memoria, por lo que dicho objeto se asigna a la variable $a.

La configuración de la desviación de medios se almacena junto a las opciones de configuración de redes. Por consiguiente, en la línea 2 del ejemplo, guardamos los cambios realizados en la configuración de la desviación de medios en la configuración de redes llamando al cmdlet **Set-CsNetworkConfiguration** y pasando el objeto de configuración de desvío de medios ($a) que hemos creado en la línea 1 al parámetro MediaBypassSettings.

    $a = New-CsNetworkMediaBypassConfiguration -AlwaysBypass $true -Enabled $true
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## EJEMPLO 2

No existe ningún cmdlet **Set-CsNetworkMediaBypassConfiguration** en Lync Server; por lo tanto, para modificar la configuración existente, deberá crear una nueva configuración (como se muestra en el ejemplo 1) para sustituir la configuración existente, o bien modificar la configuración recuperando la configuración existente, modificándola y, a continuación, usando el cmdlet **Set-CsNetworkConfiguration** para guardar los cambios. En este ejemplo se demuestra cómo desactivar la opción Always Bypass mediante esta última opción.

La primera línea del ejemplo recupera la configuración de desvío de medios existente. Lo hace llamando al cmdlet **Get-CsNetworkConfiguration**. La llamada a este cmdlet está entre paréntesis para garantizar que el cmdlet se complete antes de que se ejecute cualquier otra parte del comando. El cmdlet **Get-CsNetworkConfiguration** recupera todas las opciones de configuración de una red completa. Como solo nos interesa la configuración de desvío de medios, especificamos la propiedad MediaBypassSettings para recuperar únicamente esas opciones, las cuales se asignan a la variable $b.

En la línea 2, modificamos las configuraciones almacenadas en la variable $a mediante la asignación del valor False ($false) a la propiedad AlwaysBypass. Por último, en la línea 3, llamamos al cmdlet **Set-CsNetworkConfiguration**, pasando el parámetro MediabypassSettings a la variable $a, que guarda el cambio que hemos realizado en la propiedad AlwaysBypass.

    $a = (Get-CsNetworkConfiguration).MediaBypassSettings
    $a.AlwaysBypass = $false
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## Descripción detallada

Este cmdlet crea configuraciones globales para la desviación de medios de conexiones de audio.

A diferencia de la mayoría de cmdlets New- de Lync Server, este cmdlet no guarda de manera inmediata la nueva configuración, sino que la crea únicamente en la memoria. El objeto creado por este cmdlet debe guardarse en una variable y, a continuación, asignarse a la propiedad MediaBypassSettings de la configuración de red. (Para obtener más información, vea los ejemplos de este tema.)

Las configuraciones creadas en este cmdlet solo se podrán recuperar obteniendo acceso a la propiedad MediaBypassSettings de la configuración de red global. Para recuperar estas configuraciones, ejecute este comando: (Get-CsNetworkConfiguration).MediaBypassSettings.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **New-CsNetworkMediaBypassConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkMediaBypassConfiguration"}

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
<td><p><em>AlwaysBypass</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Si se establece este parámetro en True, se intentará realizar la desviación de medios de todas las llamadas.</p>
<p>Establezca este valor de parámetro en True únicamente si el control de admisión de llamadas (CAC) se ha deshabilitado. Establezca este parámetro en True únicamente en aquellas implementaciones en las que:</p>
<p>- No es necesario controlar el ancho de banda.</p>
<p>- No se necesita una configuración específica para saber cuándo debe producirse el desvío.</p>
<p>- Existe plena conectividad entre las puertas de enlace y los clientes.</p>
<p>Si el parámetro Enabled está establecido en True y AlwaysBypass, en False, la lógica de desvío usará los sitios y las regiones de configuración de red para saber cuándo es factible realizar el desvío.</p>
<p>Si establece AlwaysBypass en True, pero no se establece también el valor de parámetro Enabled en True, recibirá un mensaje de advertencia: La opción AlwaysBypass se ignora si Enabled está establecido en False.</p>
<p>Si se establece tanto AlwaysBypass como Enabled en True, se generará automáticamente un Id. de desvío que se almacenará en la propiedad BypassID.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Id. de la desviación de medios. Si el parámetro AlwaysBypass está establecido en True y se ha proporcionado un valor para este parámetro, BypassID se asociará a todas las subredes. Si AlwaysBypass es False, el valor de BypassID se asociará a todas las subredes que no estén en los sitios y regiones de configuración de red.</p>
<p>Este Id. debe estar en el formato GUID (por ejemplo, 96f14dea-5170-429a-b92b-f1cb909c4bb6). Con todo, por lo general no tendrá que definir o cambiar este parámetro. Este valor se genera automáticamente cuando Enabled está establecido en True y: 1) AlwaysBypass está establecido en True, o bien 2) el parámetro EnableDefaultBypassID está establecido en True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Establezca este parámetro en True para habilitar la desviación de medios. En este punto, las decisiones de desvío se basarán en el valor de la opción AlwaysBypass del siguiente modo:</p>
<p>- Si AlwaysBypass es True, trate de realizar el desvío en todas las llamadas.</p>
<p>- Si AlwaysBypass es False, use el sitio y región de configuración de red para saber si el desvío es factible.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDefaultBypassID</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Este valor se aplica únicamente si ignora si AlwaysBypass está establecido en False.</p>
<p>Si se establece este valor en True, se generará automáticamente un ID de desvío predeterminado. Este valor generado automáticamente se almacenará en la propiedad BypassID.</p>
<p>Este parámetro resulta útil cuando existe un núcleo con buenas conexiones a los sitios remotos que tienen vínculos restringidos de ancho de banda. El administrador deberá definir únicamente las subredes asociadas a los sitios remotos a través de los sitios y regiones de configuración de red. No será necesario definir ninguna subred asociada al núcleo y se intentará realizar el desvío entre dichas subredes de manera automática.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnabledForAudioVideoConferences</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Indica si se debe usar el desvío de medios para las conferencias de audio y vídeo. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalBypassMode</em></p></td>
<td><p>Opcional</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>Reservada para uso futuro. No se admite la desviación de medios externos en Lync Server.</p>
<p>Valor predeterminado: Desactivado</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalBypassMode</em></p></td>
<td><p>Opcional</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>El valor de este parámetro controla cuándo los clientes que se conectan desde la red de la organización pueden intentar llevar a cabo un desvío de medios. Si Enabled está establecido en True, este valor cambiará automáticamente a Any. El resto de valores de este parámetro se reserva para uso futuro.</p>
<p>Valor predeterminado: Desactivado</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Crea una referencia de objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.MediaBypassSettingsType.

## Vea también

#### Otros recursos

[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)

