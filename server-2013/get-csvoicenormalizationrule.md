---
title: Get-CsVoiceNormalizationRule
TOCTitle: Get-CsVoiceNormalizationRule
ms:assetid: 59fe1370-1cec-4cf9-8f65-029a7c2454d1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398393(v=OCS.15)
ms:contentKeyID: 48275372
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceNormalizationRule

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre las reglas de normalización de voz usadas en la organización. Las reglas de normalización convierten requisitos de marcado de teléfono (por ejemplo, marcar 9 para obtener acceso a una línea externa) al formato de número de teléfono E.164 usado por Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceNormalizationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se recuperan todas las reglas de normalización de voz definidas en la organización.

    Get-CsVoiceNormalizationRule

## EJEMPLO 2

En el ejemplo 2 se recuperan todas las reglas de normalización de voz especificadas para todos los sitios.

    Get-CsVoiceNormalizationRule -Filter site*

## EJEMPLO 3

El Ejemplo 3 recupera todas las reglas de normalización de voz con la letra s en el ámbito. Por ejemplo, esto devolverá todas las reglas en el nivel del sitio y de servicio, y las reglas por usuario con una s en el nombre del ámbito, tal como RedmondEastUsers.

    Get-CsVoiceNormalizationRule -Filter *s*

## EJEMPLO 4

El parámetro Filter de los ejemplos 2 y 3 solo coincide con la parte del ámbito del parámetro Identity. En este ejemplo se realiza una coincidencia con la parte del nombre para devolver todas las reglas cuyo parámetro Name contiene la cadena "seattle". En primer lugar, se llama al cmdlet **Get-CsVoiceNormalizationRule** para recuperar todas las reglas de normalización de la organización. A continuación, esta colección se canaliza al cmdlet **Where-Object** para buscar todos los elementos de la colección cuya propiedad Name coincide con la cadena "seattle".

    Get-CsVoiceNormalizationRule | Where-Object {$_.Name -match "seattle"}

## Descripción detallada

Este cmdlet devuelve una regla o una recopilación de reglas de normalización de voz. Estas reglas son un componente necesario de la autorización telefónica y el enrutamiento de llamadas. Definen los requisitos de conversión (o traducción) de números de un formato Lync Server interno a un formato estándar (E.164). Conocer las expresiones regulares facilita la definición de los patrones de números que se traducirán.

Puede obtener acceso a las mismas reglas a las que se tiene acceso con este cmdlet mediante la propiedad NormalizationRules devuelta por una llamada al cmdlet **Get-CsDialPlan**.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar el cmdlet **Get-CsVoiceNormalizationRule** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceNormalizationRule"}

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
<td><p>Usa cadenas comodín para devolver una recopilación de reglas de normalización basadas en Identity. Tenga en cuenta que el filtro solamente afecta a la sección de ámbito de la Identidad, no al nombre. Por ejemplo, el valor de filtro *lob* devolverá todas las reglas que tengan el ámbito global en su identidad (ámbitos que contienen las letras &quot;lob&quot;), pero no una regla con la identidad site:Redmond/lobby, en la que lob es solamente una parte del nombre de la identidad, no el ámbito.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único de la regla. Si se especifica un valor para este parámetro, debe tener el formato ámbito/nombre; por ejemplo, site:Redmond/Rule1, site:Redmond es el ámbito y Rule1 es el nombre.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la regla de normalización de voz de la réplica local de la Almacén de administración central, en lugar de la Almacén de administración central en sí.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Get-CsVoiceNormalizationRule** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Vea también

#### Otros recursos

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Get-CsDialPlan](get-csdialplan.md)

