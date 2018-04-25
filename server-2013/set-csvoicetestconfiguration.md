---
title: Set-CsVoiceTestConfiguration
TOCTitle: Set-CsVoiceTestConfiguration
ms:assetid: 7b95fc95-ec0e-4bb3-aed1-e8b72e305999
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398614(v=OCS.15)
ms:contentKeyID: 48275776
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceTestConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica una situación de prueba que puede usar para probar números de teléfono con rutas y reglas especificadas. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceTestConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo, se define el número marcado de la configuración de prueba de voz TestConfig1 como 14255551212. Este es el número que se comprobará con la directiva de voz y la ruta para garantizar que la normalización se realiza correctamente y asegurar que se usan las rutas y planes de marcado correctos.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 14255551212

## Ejemplo 2

En este ejemplo, se modifican los parámetros de la configuración de prueba de voz TestConfig1. El comando define el valor de TargetDialplan como el plan de marcado de site:Redmond1. Como un cambio en el plan de marcado podría suponer un cambio en las reglas de normalización, también se ha cambiado el valor ExpectedTranslationNumber para reflejar lo que se espera de las reglas de normalización del plan de marcado.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -TargetDialplan site:Redmond1 -ExpectedTranslatedNumber "+912065551212"

## Descripción detallada

Antes de implementar rutas y directivas de voz, es recomendable probarlas en varios números de teléfono para garantizar los resultados esperados. Puede hacerlo modificando situaciones de prueba con este cmdlet.

El cmdlet **Set-CsVoiceTestConfiguration** modifica la ruta de voz, el uso, el plan de marcado y la directiva de voz usados para probar un número de teléfono especificado. Toda esta información puede definirse y recuperarse con otros cmdlets, según se especifica en las descripciones de parámetros de este tema.

Las configuraciones modificadas con este cmdlet se prueban con el cmdlet **Test-CsVoiceTestConfiguration**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para iniciar el cmdlet **Set-CsVoiceTestConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceTestConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DialedNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>El número de teléfono que quiere usar para probar directivas, usos, etc.</p>
<p>Debe tener 512 caracteres o menos.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>El nombre de la ruta de voz que debe usarse durante la prueba de configuración. Si se usa otra ruta, basada en el plan de marcado de destino y la directiva de voz, la prueba fallará. Puede recuperar rutas de voz disponibles llamando al cmdlet <strong>Get-CsVoiceRoute</strong>.</p>
<p>Debe tener 256 caracteres o menos.</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>El número de teléfono en el formato con el que debe verse después de la traducción. Es el valor del parámetro DialedNumber después de la normalización. Si se ejecuta el cmdlet <strong>Test-CsVoiceTestConfiguration</strong> y DialedNumber no da como resultado el valor de ExpectedTranslatedNumber, la prueba dará error.</p>
<p>Debe tener 512 caracteres o menos.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>El nombre del uso de la RTC que se espera usar durante la prueba de configuración. Si se usa otra RTC según el plan de marcado de destino y la directiva de voz, la prueba dará error. Puede recuperar los usos disponibles si llama al cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Debe tener 256 caracteres o menos.</p></td>
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
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Una cadena de caracteres que identifica de manera única la situación de prueba que se quiere modificar.</p>
<p>El valor de este parámetro no incluye el ámbito porque este objeto solo puede crearse en el ámbito global. Por lo tanto, solo se necesita un nombre.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>TestConfiguration</p></td>
<td><p>Un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration que contiene una configuración de prueba de voz con los cambios que quiere realizar en ella. Se puede recuperar un objeto de este tipo al llamar al cmdlet <strong>Get-CsVoiceTestConfiguraton</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetDialplan</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La identidad del plan de marcado que se usará para la prueba. Los planes de marcado pueden recuperarse llamando al cmdlet <strong>Get-CsDialPlan</strong>.</p>
<p>Debe tener 40 caracteres o menos.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La identidad de la directiva de voz con la que se ejecutará la prueba. Las directivas de voz pueden recuperarse llamando al cmdlet <strong>Get-CsVoicePolicy</strong>.</p>
<p>Debe tener 40 caracteres o menos.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration. Acepta la entrada canalizada de objetos de configuración de prueba de voz.

## Tipos de valores devueltos

Este cmdlet devuelve un objeto del tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration.

## Vea también

#### Otros recursos

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

