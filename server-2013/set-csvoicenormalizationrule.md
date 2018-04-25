---
title: Set-CsVoiceNormalizationRule
TOCTitle: Set-CsVoiceNormalizationRule
ms:assetid: 68850abb-4ac7-4ae1-bb6e-d991385f92a4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398491(v=OCS.15)
ms:contentKeyID: 48275558
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceNormalizationRule

 

_**Última modificación del tema:** 2015-03-09_

Modifica una regla de normalización de voz. Las reglas de normalización de voz se usan para convertir un requisito de marcado de teléfono (por ejemplo, marcar 9 para obtener acceso a una línea externa) al formato de número de teléfono E.164 usado por Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceNormalizationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

Este ejemplo define la descripción de la regla Prefix Redmond en el sitio Redmond: "Add a prefix to all numbers on site Redmond" (Agregar un prefijo a todos los números del sitio Redmond).

    Set-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond" -Description "Add a prefix to all numbers on site Redmond"

## EJEMPLO 2

En este ejemplo se modifica la regla de normalización de voz con el parámetro Identity establecido en global/SeattleFourDigit. Se ha especificado una nueva descripción para reflejar las modificaciones realizadas en la regla. Asimismo, se ha especificado un valor Translation que modifica la regla para traducir cualquier número que coincida con el patrón existente de la regla al mismo número pero con el prefijo +1206556. Por ejemplo, si el patrón existente coincidiera con cualquier número de cuatro dígitos y se hubiera introducido el número 1234, la regla traduciría la extensión al número +12065561234.

    Set-CsVoiceNormalizationRule -Identity global/SeattleFourDigit -Description "Translate an internal four-digit extension" -Translation '+1206556$1'

## EJEMPLO 3

En el ejemplo 3, se cambia el nombre de la regla de normalización. Recuerde que al cambiar el nombre, cambia también la parte del nombre de la Identidad (Identity). El cmdlet **Set-CsVoiceNormalizationRule** no tiene un parámetro Name, de modo que para cambiar el nombre primero se llama al cmdlet **Get-CsVoiceNormalizationRule** para recuperar la regla con el valor de Identity global/RedmondFourDigit y asignar el objeto devuelto a la variable $a. La cadena de caracteres RedmondRule se asigna luego a la propiedad Name del objeto. Después, se envía la variable al parámetro Instance del cmdlet **Set-CsVoiceNormalizationRule** para que el cambio sea permanente.

    $a = Get-CsVoiceNormalizationRule -Identity global/RedmondFourDigit
    $a.name = "RedmondRule"
    Set-CsVoiceNormalizationRule -Instance $a

## Descripción detallada

Este cmdlet modifica una regla de normalización de voz con nombre. Estas reglas son un componente necesario de la autorización telefónica y el enrutamiento de llamadas. Definen los requisitos de conversión (o traducción) de números de un formato de Lync Server interno a un formato estándar (E.164). Conocer las expresiones regulares facilita la definición de los patrones de números que se traducirán.

Las reglas que se modifican usando este cmdlet forman parte del plan de marcado y, además de ser accesibles a través del cmdlet **Get-CsVoiceNormalizationRule**, también puede obtenerse acceso a ellas a través de la propiedad NormalizationRules que se devuelve tras una llamada al cmdlet **Get-CsDialPlan**.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsVoiceNormalizationRule** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceNormalizationRule"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Una descripción sencilla de la regla de normalización.</p>
<p>Longitud máxima de la cadena de caracteres: 512 caracteres.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único de la regla. El parámetro Identity especificado debe incluir el ámbito seguido de una barra y después el nombre, por ejemplo: site:Redmond/Rule1, donde site:Redmond es el ámbito y Rule1 es el nombre.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>NormalizationRule</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes. Este objeto debe ser de tipo NormalizationRule y se puede recuperar llamando al cmdlet <strong>Get-CsVoiceNormalizationRule</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>IsInternalExtension</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si el valor es True, el resultado de la aplicación de esta regla será un número interno de la empresa. Si el valor es False, el resultado de la aplicación de la regla será un número externo. Este valor se omite en caso de que el valor de la propiedad OptimizeDeviceDialing del plan de marcado asociado esté establecido en False.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Expresión regular con la que debe coincidir el número marcado para que se aplique la regla.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Int32</p></td>
<td><p>El orden en que se aplican las reglas. Un número puede coincidir con más de una regla. Este parámetro establece el orden en que se prueban las reglas con el número.</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>El patrón de expresión regular que se aplicará al número para convertirlo al formato E.164.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule. El cmdlet **Set-CsVoiceNormalizationRule** acepta entradas canalizadas de objetos de regla de normalización de voz.

## Tipos de valores devueltos

El cmdlet **Set-CsVoiceNormalizationRule** no devuelve un valor u objeto. En su lugar, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Vea también

#### Otros recursos

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

