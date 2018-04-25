---
title: Set-CsVoicemailReroutingConfiguration
TOCTitle: Set-CsVoicemailReroutingConfiguration
ms:assetid: c16a0d47-318b-46e4-991c-e4842403dbe3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412948(v=OCS.15)
ms:contentKeyID: 48276553
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicemailReroutingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica las opciones de configuración que proporcionan los números de teléfono de la red telefónica conmutada (RTC) para obtener acceso a las características Acceso de suscriptor y Operador automático de Mensajería unificada de Exchange. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicemailReroutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se habilitan las opciones de configuración de desvío de correo de voz para el sitio Redmond1.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True

## Ejemplo 2

En este ejemplo se modifica la configuración de desvío de correo de voz que se aplica al sitio Redmond1 y se define el número de teléfono para Acceso de suscriptor en +14255551213.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## Descripción detallada

Este cmdlet permite modificar la configuración que determina donde se desvían las llamadas de Acceso de suscriptor y Operador automático cuando se pierde la conectividad IP con un servidor de Mensajería unificada de Exchange.

Operador automático y Acceso de suscriptor son características de Mensajería unificada de Exchange. La característica Operador automático proporciona prestaciones de reconocimiento de voz y control por tonos (tono de marcado de frecuencia múltiple, DTMF) para que los autores de llamadas externos naveguen por el sistema telefónico de una compañía y, así, puedan ponerse en contacto con el departamento o empleado deseado, o bien, en el modo de toma de mensajes (Message Taking), aceptar mensajes para los usuarios. (Para el modo de toma de mensajes se recomienda el desvío de voz). Acceso de suscriptor permite a los usuarios internos obtener acceso a su buzón de correo de Microsoft Outlook desde un teléfono. Los números proporcionados por esta configuración permiten a los autores de las llamadas dejar mensajes de correo de voz para los usuarios de telefonía IP empresarial (la opción de configuración AutoAttendantNumber), así como recuperar correo de voz a dichos usuarios, aunque la conectividad IP de la implementación de Lync Server con la Mensajería unificada de Exchange en un sitio remoto no esté disponible en el centro de datos (la opción de configuración SubscriberAccessNumber).

Tenga en cuenta que está configuración no está disponible, a menos que la propiedad Enabled se haya definido en True.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsVoicemailReroutingConfiguration** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles RBAC a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicemailReroutingConfiguration"}

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
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Número de teléfono del operador automático al que deben desviarse los intentos del depósito de correo de voz.</p>
<p>El número proporcionado para este parámetro debe ser un LineUri de un objeto de contacto existente.</p>
<p>El valor debe ser un número que comience por un dígito de 1 a 9, que puede ir precedido de un signo más (+) y seguido de un número cualquiera de dígitos.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si los intentos para obtener acceso al correo de voz deben desviarse a través de la RTC si se pierde la conectividad IP.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>El identificador único de la configuración que se quiere modificar. Para este cmdlet la identidad será Global o Site:&lt;nombre del sitio&gt;, donde &lt;nombre del sitio&gt; es el nombre del sitio al que se aplica la configuración.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>VoicemailReroutingConfiguration</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes.</p>
<p>Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration (que puede recuperarse llamando al cmdlet <strong>Get-CsVoicemailReroutingConfiguration</strong>).</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>El número de acceso del suscriptor al que deben desviarse los intentos de recuperación de correo de voz.</p>
<p>El número proporcionado para este parámetro debe ser un LineUri de un objeto de contacto existente.</p>
<p>El valor debe ser un número que comience por un dígito de 1 a 9, que puede ir precedido de un signo más (+) y seguido de un número cualquiera de dígitos.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration. Acepta la entrada canalizada de objetos de configuración para el desvío de correo de voz.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Vea también

#### Otros recursos

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

