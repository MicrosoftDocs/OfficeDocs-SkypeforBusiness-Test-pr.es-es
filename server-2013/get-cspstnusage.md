---
title: Get-CsPstnUsage
TOCTitle: Get-CsPstnUsage
ms:assetid: 9dc82b88-303b-4678-8298-0dbc769f6781
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412734(v=OCS.15)
ms:contentKeyID: 48276229
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPstnUsage

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los registros de uso de las redes telefónicas conmutadas (RTC) que se usan en la organización. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPstnUsage [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

Este comando devuelve la lista de usos de RTC globales que hay disponibles en una organización.

    Get-CsPstnUsage

## Ejemplo 2

El comando de este ejemplo devuelve una lista de todos los usos de las RTC definidas con un uso especificado en cada línea del resultado. Al llamar al mismo cmdlet **Get-CsPstnUsage**, se devuelve el valor de Identity y la lista de usos. Si la lista de usos contiene más de tres o cuatro entradas, se abreviará en el resultado, de una forma similar a esta:

Usage : {Internal, Local, Long Distance, International...}

Use el comando de este ejemplo para mostrar solo una lista de usos. El resultado será similar a este:

Internal

Local

Long Distance

International

Restricted

    (Get-CsPstnUsage).Usage

## Ejemplo 3

Este comando devuelve todos los nombres de usos de RTC que contienen la cadena de caracteres "tern" en algún lugar del nombre. Por ejemplo, devolverá los nombres "Internal" e "International", pero no los nombres "Local" o "Long Distance".

La primera parte de este comando es el cmdlet **Get-CsPstnUsage** entre paréntesis, lo que significa que todos los usos de RTC deben recuperar la primera cosa que sucede. La propiedad .Usage solo devuelve la información de uso sobre los usos de RTC, no el valor de Identity. A continuación, la lista de usos se transfiere al cmdlet **ForEach-Object**, que analiza las cadenas de caracteres de usos una por una. La instrucción If compara la cadena de caracteres de uso actual con la cadena de caracteres "\*tern\*" (el \* son caracteres comodín) y muestra las repeticiones que coinciden con el patrón.

    (Get-CsPstnUsage).Usage | ForEach-Object {if ($_ -like "*tern*") {$_}}

## Descripción detallada

Los usos de RTC son valores de cadenas de caracteres que se usan para la autorización de llamadas. Un uso de RTC vincula una directiva de voz con una ruta. El cmdlet **Get-CsPstnUsage** recupera la lista de todos los usos de RTC disponibles en una organización.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **Get-CsPstnUsage** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPstnUsage"}

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
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>El parámetro Filter permite recuperar únicamente los usos de RTC con un valor de Identity que coincida con una cadena comodín concreta. No obstante, el único valor de Identity disponible para los usos de RTC es Global, por lo que este parámetro no es útil para este cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>El nivel en el que se aplican estas configuraciones. La única identidad que se puede aplicar a los usos de RTC es Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera información de uso de RTC del almacenamiento de datos locales en lugar de Almacén de administración central principal.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Get-CsPstnUsage** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PSTNUsages.

## Vea también

#### Otros recursos

[Set-CsPstnUsage](set-cspstnusage.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

