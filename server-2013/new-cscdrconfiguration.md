---
title: New-CsCdrConfiguration
TOCTitle: New-CsCdrConfiguration
ms:assetid: e5890ac3-7a6c-4609-a866-84c39b76d3a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399018(v=OCS.15)
ms:contentKeyID: 48277002
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCdrConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea un conjunto de configuraciones de registro de detalles de llamada (CDR). El CDR permite realizar un seguimiento del uso de ciertos elementos como, por ejemplo, las sesiones de mensajería instantánea punto a punto, las llamadas telefónicas de voz sobre IP (VoIP) y las llamadas de conferencia. Los datos de uso incluyen información sobre quién llamó a quién, cuándo llamó y cuánto tiempo hablaron. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 usa el cmdlet **New-CsCdrConfiguration** para crear un conjunto de configuraciones del CDR con la identidad site:Redmond. Además de la identidad site:Redmond, la nueva configuración también establece la propiedad EnableCDR en False. Dado que la configuración del sitio tiene preferencia sobre la configuración global, el CDR no se usará en el sitio Redmond, al margen de si el CDR está habilitado en el ámbito global.

    New-CsCdrConfiguration -Identity site:Redmond -EnableCDR $False

## Ejemplo 2

En el ejemplo 2 se muestra cómo usar el parámetro InMemory para crear una nueva recopilación de opciones de configuración del CDR que, inicialmente, solo existen en la memoria. Para ello, el ejemplo usa primero el cmdlet **New-CsCdrConfiguration** y el parámetro InMemory para crear una recopilación virtual de configuraciones con la identidad site:Redmond. Esta recopilación virtual se almacena en la variable $x; si no se almacenase en una variable, desaparecería inmediatamente después de haberla creado.

Una vez creada la recopilación virtual, el comando de la línea 2 define el valor de la propiedad EnableCDR como False ($False). En la línea 3, se usa el cmdlet **Set-CsCdrConfiguration** para transformar la recopilación virtual $x en una recopilación real de opciones de configuración del CDR que se aplica al sitio Redmond. Si no se llamara al cmdlet **Set-CsCdrConfiguration**, la recopilación virtual desaparecería al finalizar la sesión de Windows PowerShell o eliminar la variable $x.

    $x = New-CsCdrConfiguration -Identity site:Redmond -InMemory
    $x.EnableCDR = $False
    Set-CsCdrConfiguration -Instance $x

## Descripción detallada

El registro detallado de llamadas (CDR) permite controlar el uso de algunas funciones de Lync Server, como las llamadas telefónicas de voz sobre IP (VoIP), la mensajería instantánea (MI), las transferencias de archivos, las conferencias de audio/vídeo (A/V) y las sesiones de aplicaciones compartidas. El CDR (disponible solo si se ha implementado el servicio de supervisión) realiza un seguimiento de la información de uso: registra información como los interlocutores de la llamada, la duración y si se ha transferido algún archivo. (Sin embargo, el CDR no graba las llamadas en sí.)

También se registra la información de errores de llamadas: datos de diagnóstico detallados de sesiones punto a punto y llamadas de conferencia.

Como administrador, puede decidir si se usará o no el CDR en la organización; si se ha implementado el servicio de supervisión, puede habilitar o deshabilitar el CDR fácilmente. Además, puede tomar esta decisión de manera global (en cuyo caso CDR se habilitará o se deshabilitará en toda la organización) o sitio por sitio; por ejemplo, puede usar CDR en Redmond site, pero en Paris site.

El cmdlet **New-CsCdrConfiguration** permite crear recopilaciones de configuraciones del CDR en el ámbito de sitio. (No se pueden crear configuraciones en el ámbito global.) Cada sitio puede hospedar solamente una recopilación de configuraciones del CDR. Por lo tanto, no puede crear una nueva recopilación para el sitio Redmond si ya hay un conjunto de configuraciones de registro de llamadas en dicho sitio. Si lo intenta, el comando fallará.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **New-CsCdrConfiguration** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCdrConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Requerido</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Representa el identificador único que se asignará a la nueva recopilación de configuraciones de registro de llamadas. Como solo puede crear nuevas colecciones en el ámbito del sitio, la Identidad siempre será el prefijo &quot;site:&quot; seguido del nombre del sitio; por ejemplo &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCDR</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica si está habilitado el CDR. El valor predeterminado es True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica si los registros del CDR se eliminarán periódicamente de la base de datos del CDR. Si se define como True (el valor predeterminado), los registros se eliminarán una vez transcurrido el período de tiempo especificado mediante las propiedades KeepCallDetailForDays (registros del CDR) y KeepErrorReportForDays (errores del CDR). Si se define como False, los registros de detalles de llamadas se conservarán indefinidamente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean irrecuperables y que puedan surgir al ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica el número de días que los registros del CDR se conservarán en la base de datos del CDR; los registros con una antigüedad superior al número de días especificado se eliminarán automáticamente. (Tenga en cuenta que la depuración solo se llevará a cabo si la propiedad EnablePurging se ha definido como True.)</p>
<p>KeepCallDetailForDays puede definirse como cualquier valor entero entre 1 y 2562 días (aproximadamente 7 años). El valor predeterminado es 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica el número de días que se conservarán los informes de errores del CDR; cualquier informe con una antigüedad superior al número de días especificado se eliminará automáticamente. Los informes de errores del CDR son informes de diagnóstico cargados por aplicaciones cliente, como Lync 2013.</p>
<p>Puede definir esta propiedad como cualquier valor entero entre 1 y 2562 días (aproximadamente 7 años). El valor predeterminado es 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la hora local en que se eliminan los registros expirados de la base de datos de registro. La hora del día se especifica con un reloj de 24 horas, donde 0 representa la medianoche (12 de la noche) y 23 representa las 11 de la noche. Tenga en cuenta que solamente puede especificar la hora del día; es decir, puede programar el purgado para que se realice a las 4 de la mañana, pero no a las 4:30 o las 4:15. El valor predeterminado es 2 (2 de la mañana). Es recomendable realizar la depuración en horario no laboral.</p>
<p>La depuración de la base de datos solo se lleva a cabo si la propiedad EnablePurging está definida en True.</p></td>
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

Ninguno. El cmdlet **New-CsCdrConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

Crea instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Vea también

#### Otros recursos

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

