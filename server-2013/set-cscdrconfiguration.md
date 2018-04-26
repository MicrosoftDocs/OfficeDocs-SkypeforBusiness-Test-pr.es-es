---
title: Set-CsCdrConfiguration
TOCTitle: Set-CsCdrConfiguration
ms:assetid: 977f0d3e-796b-43a3-bc0c-82ea91741c52
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398774(v=OCS.15)
ms:contentKeyID: 48276094
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCdrConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica una colección de configuraciones de registro de detalles de llamada (CDR). CDR permite controlar, por ejemplo, el uso de sesiones de mensajería instantánea de punto a punto, las llamadas de teléfono de voz sobre IP (VoIP) y las llamadas de conferencias. Estos datos de uso incluyen información sobre quién ha llamado a quién, cuándo y durante cuánto tiempo han hablado. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCdrConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El ejemplo anterior define la hora del día en que se purgarán los registros antiguos. En este caso, se ha fijado la hora en 23 (11:00 p. m. en el formato de 24 horas). El parámetro Identity se usa para garantizar que estos cambios se apliquen solo a las configuraciones de CDR cuya identidad sea site:Redmond.

    Set-CsCdrConfiguration -Identity site:Redmond -PurgeHourOfDay 23 

## Ejemplo 2

El ejemplo 2 es una variación del comando que se muestra en el ejemplo 1. En este caso, la propiedad PurgeHourOfDay se modifica en todas las colecciones de opciones de configuración de CDR que usa actualmente la organización. Para hacerlo, se llama primero al comando **Get-CsCdrConfiguration** sin ningún parámetro para devolver una colección de todas las configuraciones de CDR que están en uso. Luego, se canaliza esta colección al cmdlet **Set-CsCdrConfiguration**, que cambia en todos los elementos de la colección la propiedad PurgeHourOfDay a las 11:00 p. m. (23).

    Get-CsCdrConfiguration | Set-CsCdrConfiguration -PurgeHourOfDay 23 

## Ejemplo 3

Otra variación del comando usado en el ejemplo 1 se muestra en el ejemplo 3. En este caso, la propiedad PurgeHourOfDay se cambia en todas las configuraciones de CDR definidas en el ámbito de sitio. Para llevar a cabo esta tarea, el comando llama primero al cmdlet **Get-CsCdrConfiguration** con el parámetro Filter; el valor de filtro "site:\*" garantiza que solo se devolverá la configuración de CDR que tiene una identidad que comienza con el valor de cadena "site:". La colección filtrada se canaliza al cmdlet **Set-CsCdrConfiguration**, que modifica la propiedad PurgeHourOfDay de todos los elementos de esa colección.

    Get-CsCdrConfiguration -Filter "site:*"| Set-CsCdrConfiguration -PurgeHourOfDay 23

## Descripción detallada

El registro de detalles de llamadas (CDR) permite controlar el uso de funciones de Lync Server, como llamadas telefónicas de voz sobre IP (VoIP), mensajería instantánea (MI), transferencias de archivos, conferencias de audio/vídeo (A/V) y sesiones de aplicaciones compartidas. El CDR (disponible únicamente si se ha implementado el servicio de supervisión) guarda la información de uso: registra información como las partes que intervienen en la llamada, la duración de la llamada y si se han transferido archivos. Sin embargo, el CDR no registra la llamada propiamente dicha.

Por otra parte, el CDR realiza un seguimiento de la información de errores: datos de diagnóstico detallados de sesiones de punto a punto y conferencias.

Como un administrador, puede determinar si se usa o no CDR en la organización; si se asume que el servicio de supervisión se implementó, puede habilitar o deshabilitar CDR rápidamente. Además, se puede tomar la decisión de forma global (en cuyo caso, el CDR estará habilitado o deshabilitado en toda la organización) o sitio por sitio. Por ejemplo, se puede utilizar el CDR en el sitio de Redmond, pero no en el de París.

Los administradores también pueden administrar la base de datos de CDR, por ejemplo, especificando la cantidad de días que se mantienen los registros de CDR antes de purgarse de la base de datos. Se pueden realizar cambios como estos con el cmdlet **Set-CsCdrConfiguration**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsCdrConfiguration** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCdrConfiguration"}

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
<td><p><em>EnableCDR</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica si el CDR está habilitado. El valor predeterminado es True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica si los registros de CDR se eliminarán periódicamente de la base de datos de registro. Si se define como True (valor predeterminado), los registros se eliminarán una vez transcurrido el período de tiempo especificado con las propiedades KeepCallDetailForDays (para los registros CDR) y KeepErrorReportForDays (para errores de CDR). Si es False, los registros de CDR se mantendrán por tiempo indefinido.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único asignado a la colección de opciones de configuración de CDR. Para hacer referencia a la configuración global, use la siguiente sintaxis: -Identity global. Para hacer referencia a una colección configurada en el ámbito de sitio, use una sintaxis similar a esta: -Identity site:Redmond. Tenga en cuenta que no se pueden utilizar caracteres comodín al especificar una identidad.</p>
<p>Si se omite este parámetro, el cmdlet <strong>Set-CsCdrConfiguration</strong> modificará la configuración global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>Objeto CdrSettings</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica el número de días que los registros de CDR se conservarán en la base de datos de registro; los registros con una antigüedad superior al número de días especificado se eliminarán automáticamente. (Tenga en cuenta que solo se realizará el purgado si la propiedad EnablePurging tiene el valor True).</p>
<p>Puede definir esta propiedad en cualquier valor entero entre 1 y 2562 días (aproximadamente 7 años). El valor predeterminado es 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica el número de días que se conservarán los informes de errores de CDR; cualquier informe con una antigüedad superior al número de días especificado se eliminará automáticamente. Los informes de errores de CDR son informes de diagnóstico cargados por aplicaciones cliente, como Lync 2013.</p>
<p>Puede definir esta propiedad en cualquier valor entero entre 1 y 2562 días (aproximadamente 7 años). El valor predeterminado es 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la hora local del día en que se eliminan los registros que hayan expirado de la base de datos de CDR. La hora del día se especifica con el formato de 24 horas, de modo que 0 representa la medianoche (12:00 a. m.) y 23 representa las 11:00 p.m. Tenga en cuenta que solo se puede especificar la hora del día, es decir, puede programar el purgado para las 4:00 a. m., pero no para las 4:30 a. m. ni las 4:15 a. m. El valor predeterminado es 2 (2:00 a. m.). Se recomienda realizar el purgado fuera del horario laboral.</p>
<p>Solo se realiza el purgado de la base de datos si el valor de la propiedad EnablePurging es True.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. El cmdlet **Set-CsCdrConfiguration** acepta entradas canalizadas de los objetos de configuración del registro detallado de llamadas.

## Tipos de valores devueltos

El cmdlet **Set-CsCdrConfiguration** no devuelve ningún valor ni objeto. En su lugar, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CDRSettings.

## Vea también

#### Otros recursos

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

