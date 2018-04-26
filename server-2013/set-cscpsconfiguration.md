---
title: Set-CsCpsConfiguration
TOCTitle: Set-CsCpsConfiguration
ms:assetid: 9c2c0ad1-12f8-47b6-a7ec-60d91c9685bf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412721(v=OCS.15)
ms:contentKeyID: 48276138
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCpsConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica una colección existente de configuraciones del servicio de estacionamiento de llamadas. El estacionamiento de llamadas es un servicio que permite a un usuario "estacionar" una llamada de teléfono entrante. Al estacionar una llamada, esta se transfiere a un número de un intervalo especificado u órbita y de inmediato se coloca la llamada en espera. Cualquiera (no solo la persona que respondió a la llamada originalmente) puede continuar con la conversación desde cualquier teléfono simplemente al marcar el número correcto. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCpsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 modifica la configuración del servicio de estacionamiento de llamadas con la identidad site:Redmond1 al establecer en 2 el número de veces que una llamada estacionada volverá a sonar en el teléfono en que se respondió. Para ello, se incluye el parámetro MaxCallPickupAttempts y se establece el valor de parámetro en 2.

    Set-CsCpsConfiguration -Identity site:Redmond1 -MaxCallPickupAttempts 2

## Ejemplo 2

El ejemplo 2 es una variante del comando del ejemplo 1, aunque en este caso se establece en 2 la propiedad MaxCallPickupAttempts de todas (no solo una) las configuraciones del servicio de estacionamiento de llamadas. Para ello, se usa el cmdlet **Get-CsCpsConfiguration** para recuperar una colección de todas las configuraciones del servicio de estacionamiento de llamadas que se usan en la organización. Después, esta colección se canaliza al cmdlet **Set-CsCpsConfiguration**, que establece el valor de la propiedad MaxCallPickupAttempts en 2 para todos los elementos que contiene.

    Get-CsCpsConfiguration | Set-CsCpsConfiguration -MaxCallPickupAttempts 2

## Ejemplo 3

En este ejemplo, se modifica la configuración del estacionamiento de llamadas del sitio Redmond1, estableciendo la cantidad de tiempo que pasará antes de que una llamada estacionada vuelva a sonar en 45 segundos (este valor se encuentra en la propiedad CallPickupTimeoutThreshold).

    Set-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:00:45

## Descripción detallada

Este cmdlet se usa para modificar una configuración existente del servicio de estacionamiento de llamadas. Una configuración del servicio de estacionamiento de llamadas especifica qué sucede con una llamada cuando se ha estacionado. Por ejemplo, si no se responde a una llamada estacionada en un período de tiempo, puede desviarse automáticamente a otra persona, como un administrador, o a un grupo de respuesta. Pueden configurarse las llamadas para que suene el teléfono pasado un período de tiempo para garantizar que no se olvidan. Además, puede configurar el servicio de estacionamiento de llamadas para que la persona que está en espera escuche música mientras la llamada está estacionada.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **Set-CsCpsConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCpsConfiguration"}

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
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>Opcional</p></td>
<td><p>TimeSpan</p></td>
<td><p>El tiempo que pasará después de estacionar la llamada hasta que vuelva a sonar en el teléfono en el que se respondió.</p>
<p>Debe especificarse con formato hh:mm:ss (hh = horas, mm = minutos, ss = segundos)</p>
<p>Valor mínimo: 10 segundos (00:00:10); Valor máximo: 10 minutos (00:10:00)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Determina si la persona que llama escuchará música mientras la llamada está estacionada.</p>
<p>Lync Server incluye una música predeterminada en el archivo Hold. Puede modificar este archivo para cambiar la música que oirá la persona que llama mientras la llamada está estacionada con el cmdlet <strong>Set-CsCallParkServiceMusicOnHoldFile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecen antes de hacer cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificador único de la configuración que se quiere modificar. La propiedad Identity especifica el ámbito al que se aplica la configuración: Global o un sitio específico (con el formato site:&lt;nombre_sitio&gt;, por ejemplo, site:Redmond).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>CallParkServiceSettings</p></td>
<td><p>Referencia de objeto a un objeto de configuración del servicio de estacionamiento de llamadas del tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Este objeto puede recuperarse con una llamada al cmdlet <strong>Get-CsCpsConfiguration</strong>. Después, se puede modificar y se pueden guardar los cambios al enviar el objeto de nuevo al cmdlet <strong>Set-CsCpsConfiguration</strong> en este parámetro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>El número de veces que una llamada estacionada volverá a sonar en el teléfono en que se respondió antes de desviarse a un URI de reserva. El URI de reserva se define con el parámetro OnTimeoutURI.</p>
<p>Valor mínimo: 1. Valor máximo: 10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La dirección SIP del usuario o grupo de respuesta al que se enrutarán las llamadas estacionadas que no se respondan. La llamada estacionada se enrutará cuando haya sonado tantas veces como se haya establecido en el parámetro MaxCallPickupAttempts. Si ese parámetro se configura en Null, se ignorará OnTimeoutURI y la llamada en estacionamiento se desconectará después de realizar sin éxito los intentos de devolución de llamadas.</p>
<p>Los valores deben ser identificadores URI de SIP, que comienzan por sip:. Por ejemplo, sip:rgs1@litwareinc.com.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Acepta la entrada canalizada de los objetos de la configuración del servicio de estacionamiento de llamadas

## Tipos de valores devueltos

Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vea también

#### Otros recursos

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

