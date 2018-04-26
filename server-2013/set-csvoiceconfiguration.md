---
title: Set-CsVoiceConfiguration
TOCTitle: Set-CsVoiceConfiguration
ms:assetid: dbab35ac-9a55-41d2-a726-9a26b2ff8e85
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398967(v=OCS.15)
ms:contentKeyID: 48276902
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica una lista de configuraciones de prueba de voz. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-VoiceTestConfigurations <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Para modificar una configuración de voz de prueba en una configuración de voz, se deben seguir varios pasos. En este ejemplo, se empieza recuperando el objeto de configuración de voz llamando al cmdlet **Get-CsVoiceConfiguration**. A continuación, se asigna el objeto recuperado (solo habrá uno) a la variable $a.

En la línea 2 de este ejemplo, recuperamos el contenido de la propiedad VoiceTestConfigurations, que es una colección de objetos de configuración de pruebas de voz, de la variable $a. A continuación, transferimos esa colección al cmdlet **Where-Object**, donde buscamos la colección del objeto de configuración de prueba de voz cuyo nombre sea igual a la cadena de caracteres TestConfig2. El objeto se asigna a la variable $b.

A continuación, se modifica el objeto de configuración de prueba de voz TestConfig2 asignando valores nuevos a las propiedades DialedNumber y ExpectedTranslatedNumber. Al actualizar el objeto, también se actualiza el objeto que se encuentra en la variable $a. Sin embargo, dicho objeto sigue estando únicamente en la memoria. El último paso consiste en guardar los cambios enviando la variable $a al parámetro Instance del cmdlet **Set-CsVoiceConfiguration**.

Este no es el método recomendado para modificar una configuración de voz. Para modificar una configuración de voz, cambie cada una de las configuraciones de prueba de voz mediante el cmdlet **Set-CsVoiceTestConfiguration**, como se muestra a continuación:

Set-CsVoiceTestConfiguration -Identity TestConfig2 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

Esta línea llevará a cabo la misma acción que se ha explicado en el ejemplo 1.

    $a = Get-CsVoiceConfiguration
    $b = $a.VoiceTestConfigurations | Where-Object {$_.Name -eq "TestConfig2"}
    $b.DialedNumber = "5551212"
    $b.ExpectedTranslatedNumber = "+5551212"
    Set-CsVoiceConfiguration -Instance $a

## Descripción detallada

Las configuraciones de prueba de voz se usan para probar un número de teléfono con una directiva de voz, una ruta y un plan de marcado específicos. Este cmdlet se puede usar para modificar configuraciones de prueba de voz de una lista que contenga todas las configuraciones de prueba de voz de una instalación de Lync Server.

Este cmdlet modifica un objeto del tipo VoiceConfiguration. Este objeto es simplemente un objeto contenedor para las configuraciones de prueba de voz. Por tanto, no se recomienda el uso de este cmdlet. Para modificar las configuraciones de voz, modifique las configuraciones de prueba de voz por separado llamando al cmdlet **Set-CsVoiceTestConfiguration**.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Set-CsVoiceConfiguration**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>El ámbito de este objeto. El único valor posible para este parámetro es Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>VoiceConfiguration</p></td>
<td><p>Una referencia a un objeto de configuración de voz (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration). Un objeto de este tipo puede recuperarse llamando al cmdlet <strong>Get-CsVoiceConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceTestConfigurations</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de todas las configuraciones de prueba de voz (objetos Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration) definidas para la instalación de Lync Server.</p>
<p>Para modificar los objetos de configuración de prueba de voz uno a uno, use el cmdlet <strong>Set-CsVoiceTestConfiguration</strong>. Se trata del método recomendado para modificar configuraciones de esta lista.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration. El cmdlet **Set-CsVoiceConfiguration** acepta entradas canalizadas de un objeto de configuración de voz.

## Tipos de valores devueltos

El cmdlet **Set-CsVoiceConfiguration** no devuelve ningún valor u objeto. En su lugar, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration.

## Vea también

#### Otros recursos

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

