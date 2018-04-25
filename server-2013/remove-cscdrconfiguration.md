---
title: Remove-CsCdrConfiguration
TOCTitle: Remove-CsCdrConfiguration
ms:assetid: 64352746-a03c-434a-9baf-4d9cd630e9da
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398451(v=OCS.15)
ms:contentKeyID: 48275473
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCdrConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Quita la colección especificada de opciones de configuración del registro de detalles de llamadas (CDR). CDR permite realizar un seguimiento de uso de aspectos como las sesiones de mensajería instantánea de punto a punto, llamadas telefónicas de voz sobre IP (VoIP) y llamadas en conferencia. Estos datos de uso abarcan información sobre quién llamó a quién, cuándo se llamó y la duración de la llamada. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se usa el cmdlet **Remove-CsCdrConfiguration** para quitar la configuración de CDR que se ha asignado al sitio Redmond. El uso del parámetro Identity garantiza que solo se quitarán las configuraciones que se han asignado al sitio especificado.

    Remove-CsCdrConfiguration -Identity site:Redmond

## EJEMPLO 2

El comando que se muestra en el ejemplo 2 quita todas las configuraciones de CDR que se han asignado al ámbito de sitio. En primer lugar, el comando usa el cmdlet **Get-CsCdrConfiguration** y el parámetro Filter, para recuperar las configuraciones de CDR adecuadas. El valor de cadena "site:\*" garantiza que solo se devolverán aquellos valores cuyo parámetro Identity comienza por los caracteres "site:". A continuación, la colección filtrada se canaliza al cmdlet **Remove-CsCdrConfiguration**, que elimina todos los elementos de la colección.

    Get-CsCdrConfiguration -Filter site:* | Remove-CsCdrConfiguration

## EJEMPLO 3

En el ejemplo 3 se eliminan las configuraciones de CDR cuya propiedad KeepCallDetailForDays es menor que 30 días. El comando llama al cmdlet **Get-CsCdrConfiguration** sin ningún parámetro, para devolver una colección con todas las configuraciones de CDR que actualmente se encuentran en uso en la organización. A continuación, esta colección se canaliza al cmdlet **Where-Object**, que solo selecciona las configuraciones cuya propiedad KeepCallDetailForDays es menor que 30 días. Seguidamente, la colección filtrada se canaliza al cmdlet **Remove-CsCdrConfiguration**, que elimina los distintos elementos de la colección.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30} | Remove-CsCdrConfiguration

## Descripción detallada

El registro de detalles de llamadas (CDR) permite controlar el uso de funciones de Lync Server, como las llamadas telefónicas de VoIP, la mensajería instantánea, las transferencias de archivos, las conferencias de audio/vídeo y las sesiones de aplicaciones compartidas. El CDR (disponible únicamente si se ha implementado el servicio de supervisión) guarda la información de uso: participantes de la llamada, duración de la llamada y si se han transferido archivos o no (la llamada en sí no se registra).

Por otra parte, el CDR realiza un seguimiento de la información de errores: datos de diagnóstico detallados de sesiones punto a punto y llamadas en conferencia.

En tanto que administrador, puede determinar si se usa o no CDR en la organización. Si se ha implementado el servicio de supervisión, puede habilitar o deshabilitar CDR rápidamente. Además, puede tomar esta decisión de manera global (en cuyo caso CDR se habilitará o se deshabilitará en toda la organización) o sitio por sitio; por ejemplo, puede usar CDR en Redmond site, pero en Paris site.

Las configuraciones específicas del sitio que se han creado con el cmdlet **New-CsCdrConfiguration** se pueden quitar más adelante con el cmdlet **Remove-CsCdrConfiguration**. Si se quitan configuraciones específicas del sitio, el CDR del sitio afectado se regirá de forma automática por los valores de configuración de CDR globales.

También puede ejecutar el cmdlet **Remove-CsCdrConfiguration** con la configuración de CDR global. Sin embargo, como la configuración global no se puede quitar, en su lugar se restablecerá a los valores predeterminados. Por ejemplo, supongamos que establece el valor de la propiedad KeepCallDetailForDays de la configuración global en 90. Si ejecuta el cmdlet **Remove-CsCdrConfiguration** en la configuración global, la propiedad se restablecerá a su valor predeterminado de 60.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsCdrConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCdrConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único para la configuración de CDR que se va a quitar. Para &quot;quitar&quot; la configuración global, use la siguiente sintaxis: -Identity global. (De nuevo, recuerde que en realidad la configuración global no se puede quitar, sino que únicamente se pueden restablecer las propiedades en los valores predeterminados). Para quitar la configuración del ámbito de sitio, use la sintaxis del siguiente ejemplo: -Identity site:Redmond. No puede usar caracteres comodín para especificar una identidad.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no son graves y que pueden surgir al ejecutar el comando.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. El cmdlet **Remove-CsCdrConfiguration** acepta canalizaciones de objetos de configuración de CDR.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet elimina las instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Vea también

#### Otros recursos

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

