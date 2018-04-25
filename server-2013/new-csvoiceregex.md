---
title: New-CsVoiceRegex
TOCTitle: New-CsVoiceRegex
ms:assetid: a1a498b7-8353-40bd-9c02-424c95743ec3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412751(v=OCS.15)
ms:contentKeyID: 48276170
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRegex

 

_**Última modificación del tema:** 2015-03-09_

Crea un modelo de expresión regular y de traducción para convertir los números de teléfono a distintos formatos. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsVoiceRegex -AtLeastLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    New-CsVoiceRegex -ExactLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Ejemplos

## Ejemplo 1

En este ejemplo se crean un nuevo modelo de expresión regular y una traducción. Esta expresión incluye un modelo que debe tener exactamente 7 caracteres (-ExactLength 7) y quitará los tres primeros dígitos del número correspondiente (-DigitsToStrip 3). El modelo creado con esta expresión regular será ^\\d{3}(\\d{4})$, mientras que la traducción será $1. Por ejemplo, el número 5551212 coincidiría con este modelo y la traducción resultante sería 1212: el número de 7 dígitos del que se han cortado los 3 primeros dígitos.

    $regex = New-CsVoiceRegex -ExactLength 7 -DigitsToStrip 3

## Ejemplo 2

En este ejemplo se crea también un nuevo patrón de expresión regular y conversión, pero el ejemplo va más allá y usa luego estos valores para crear una nueva regla de normalización de voz. En la primera línea se llama al cmdlet **New-CsVoiceRegEx** para crear una expresión regular en la que el número coincidente debe tener un mínimo de 7 caracteres (-AtLeastLength 7) y debe empezar con un 1 (-StartsWith "1"). Los resultados de este comando se asignan a la variable $regex.

En la segunda línea se llama al cmdlet **New-CsVoiceNormalizationRule**. Se asigna un nombre único a la nueva regla, en este caso, global/internal rule. Luego, se asigna como patrón para la regla de normalización el patrón creado al llamar al cmdlet **New-CsVoiceRegex**: -Pattern $regex.Pattern. Se hace lo mismo con la conversión y se asigna la conversión creada mediante el cmdlet **New-CsVoiceRegex**: -Translation $regex.Translation.

Nota: el modelo creado en este ejemplo es ^(1\\d{5}\\d+)$. Se puede descifrar como un número que empieza por 1 (1), seguido de cinco dígitos (\\d{5}), seguido de un número indeterminado de dígitos (\\d+). El resultado es un número de 7 dígitos como mínimo (1 más 5 más 1 ó más) que empieza por 1, justo lo que se pretendía.

    $regex = New-CsVoiceRegex -AtLeastLength 7 -StartsWith "1"
    New-CsVoiceNormalizationRule "global/internal rule" -Pattern $regex.Pattern -Translation $regex.Translation

## Descripción detallada

Las expresiones regulares se usan para asociar modelos de caracteres. Lync Server usa expresiones regulares para convertir números de teléfono en diversos formatos, incluidos los números marcados, E.164, una central de conmutación (PBX) y una red telefónica conmutada (RTC). Hasta que conozca la sintaxis y las reglas de formato para trabajar con expresiones regulares, puede resultarle complicado definir estas reglas de conversión. El cmdlet **New-CsVoiceRegex** proporciona parámetros que permiten especificar determinados criterios y luego genera la expresión regular por usted.

Use este cmdlet como ayuda para generar expresiones regulares que se deban usar como valores de patrón y conversión para reglas de normalización (el cmdlet **New-CsVoiceNormalizationRule**) y reglas de conversión saliente (el cmdlet **New-CsOutboundTranslationRule**), y valores NumberPattern para rutas de voz (el cmdlet **New-CsVoiceRoute**).

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **New-CsVoiceRegex** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRegex"}

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
<td><p><em>AtLeastLength</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Longitud mínima necesaria para que la cadena de caracteres (número de teléfono) coincida con la expresión. Por ejemplo, si define una regla de normalización que solo afecta a los números con una longitud mínima de 7 dígitos (o caracteres), especifique un valor de 7 para este parámetro.</p>
<p>Debe escribir un valor para este parámetro o para el parámetro ExactLength. No puede escribir los valores de ambos.</p></td>
</tr>
<tr class="even">
<td><p><em>ExactLength</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Longitud que debe tener la cadena de caracteres (número de teléfono) para coincidir con la expresión regular. Por ejemplo, si desea que una regla de normalización solo afecte a números de 10 dígitos, especifique el valor 10 para este parámetro.</p>
<p>Debe escribir un valor para este parámetro o para el parámetro AtLeastLength. No puede escribir los valores de ambos.</p></td>
</tr>
<tr class="odd">
<td><p><em>DigitsToPrepend</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Cadena que especifica los caracteres o los números que se deben agregar al comienzo del número de teléfono. El valor introducido para este parámetro influye en la regla de conversión, ya que antepone caracteres al número de acuerdo con el patrón de expresión regular. Por ejemplo, si el número que sigue el patrón es 5551212 y el valor DigitsToPrepend es 425, el número convertido será 4255551212 (suponiendo que no se hayan aplicado otras conversiones).</p></td>
</tr>
<tr class="even">
<td><p><em>DigitsToStrip</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Int32</p></td>
<td><p>Número de caracteres que se debe recortar al principio de la secuencia de caracteres (número de teléfono). Por ejemplo, si se escribe el número 2065551212 y DigitsToStrip es 3, el número se convertirá en 5551212</p></td>
</tr>
<tr class="odd">
<td><p><em>StartsWith</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Primer carácter de la cadena de caracteres (número de teléfono). La cadena de caracteres no coincidirá con la expresión regular a menos que empiece por la cadena de caracteres especificada en el parámetro StartsWith. Por ejemplo, si se especifica un valor de &quot;+1&quot; para StartsWith, solo los números que empiecen por +1 coincidirán con este patrón y se traducirán. Tenga en cuenta que el número de caracteres de la cadena StartsWith se incluirá en los totales ExactLength y AtLeastLenght. Por ejemplo, si ha especificado 10 para ExactLength y una cadena StartsWith de +1, un número de teléfono de acuerdo con este modelo tendría 8 caracteres de longitud, precedidos de +1, lo cual daría un total de 10 dígitos.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Crea un objeto del tipo Microsoft.Rtc.Management.Voice.OcsVoiceRegex.

## Vea también

#### Otros recursos

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)

