---
title: Set-CsOutboundTranslationRule
TOCTitle: Set-CsOutboundTranslationRule
ms:assetid: fbf82146-7884-418c-8239-66c0ca0f2ba6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg413073(v=OCS.15)
ms:contentKeyID: 48277257
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundTranslationRule

 

_**Última modificación del tema:** 2015-03-09_

Modifica una regla de conversión saliente. Las reglas de conversión salientes convierten los números de teléfono al formato de marcado local para la interacción con sistemas de central de conmutación (PBX). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este ejemplo modifica la regla de conversión saliente global con el valor de Identity site:Redmond/Prefix Redmond. Hemos incluido una descripción donde se explica que esta regla sirve para convertir números del formato E.164 a un número de teléfono de siete dígitos. Asimismo, hemos especificado los valores de Pattern y Translation, que modificarán los valores existentes de estas propiedades. Estos valores convierten un número en formato E.164 (en este caso 12 dígitos que empiezan por +1425), especificado por la expresión regular del parámetro Pattern, a un número de siete dígitos quitando los cinco primeros dígitos. Por ejemplo, el número +14255551212 se convertiría al número 5551212.

    Set-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond" -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## Ejemplo 2

En este ejemplo, se modifica la propiedad Name de una regla de conversión saliente. Tenga en cuenta que esta acción cambia el valor de Identity de esta regla. El primer comando del ejemplo es una llamada al cmdlet **Get-CsOutboundTranslationRule**. Se especifica el valor de Identity site:Redmond\\OBR1, que devolverá una regla de conversión, la regla con el valor de Identity proporcionado. En lugar de mostrar la regla, se asigna a la variable $a. En la línea 2 del ejemplo, se asigna la cadena "Outbound Rule 1" a la propiedad Name de la variable $a, que contiene una referencia a la regla site:Redmond/OBR1. En la última línea del ejemplo, se llama al cmdlet **Set-CsOutboundTranslationRule** especificando el parámetro Instance y se transfiere a la variable $a. Si se llama al cmdlet **Get-CsOutboundTranslationRule** con el valor de Identity site:Redmond/OBR1, no se devolverá nada. Esto se debe a que la regla con esta identidad ya no existe, porque se ha reemplazado por la misma regla pero con el valor de Identity site:Redmond/Outbound Rule 1.

    $a = Get-CsOutboundTranslationRule -Identity "site:Redmond/OBR1"
    $a.Name = "Outbound Rule 1"
    Set-CsOutboundTranslationRule -Instance $a

## Descripción detallada

Lync Server normaliza los números de teléfono según el formato E.164. No obstante, muchos sistemas PBX no pueden trabajar con este formato. Las reglas de conversión salientes convierten el número al formato de marcado local antes de enviar el número al Servidor de mediación o a la puerta de enlace. Llame a este cmdlet para modificar una regla de conversión de salida existente.

Cada regla de conversión saliente está asociada a una configuración de tronco. Esto significa que, al usar este cmdlet para modificar una regla, la configuración de tronco correspondiente se verá afectada. Es posible asociar más de una regla de conversión saliente a cada configuración. Por lo tanto, la identidad (Identity) de cada regla está formada por un ámbito y un nombre que es único en ese ámbito (con el formato ámbito/nombre, como site:Redmond/OBR1). La regla se asocia automáticamente a la configuración de tronco del mismo ámbito. Llamar al cmdlet **Set-CsOutboundTranslationRule** es el método recomendado para cambiar las reglas de conversión salientes de una configuración de tronco.

Quién puede ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsOutboundTranslationRule** de manera local: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC), se ha asignado este cmdlet (incluidos los roles RBAC que haya creado usted mismo) para ejecutar el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundTranslationRule"}

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
<th>Requerido</th>
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
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Una descripción detallada de la regla de conversión saliente. Esta descripción puede usarse para ayudar a los administradores a identificar claramente el propósito de la regla.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>El identificador único de la regla de conversión saliente que se quiere modificar. La identidad (Identity) está formada por el ámbito seguido de un nombre único dentro de cada ámbito. Por ejemplo, site:Redmond/OutboundRule1.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>TranslationRule</p></td>
<td><p>Una referencia de objeto a una regla de conversión saliente. Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule y puede recuperarse llamando al cmdlet <strong>Get-CsOutboundTranslationRule</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Una expresión regular que representa el patrón numérico al que se aplicará la conversión.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Si un número coincide con el patrón de más de una regla de conversión saliente, las reglas se aplicarán por orden de prioridad. Use este parámetro para asignar una prioridad a la regla.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Una expresión regular que se aplicará al número que coincida con el patrón para preparar dicho número para el enrutamiento saliente.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule. Acepta datos transferidos de objetos de reglas de conversión de salida.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Vea también

#### Otros recursos

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

