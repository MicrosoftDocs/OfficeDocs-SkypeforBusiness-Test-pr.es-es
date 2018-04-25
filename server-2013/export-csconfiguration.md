---
title: Export-CsConfiguration
TOCTitle: Export-CsConfiguration
ms:assetid: 7da7e133-e405-466c-a852-06a4fb678c59
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398627(v=OCS.15)
ms:contentKeyID: 48275798
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Exporta la topología, las directivas y las opciones de configuración de Lync Server a un archivo. Entre otras cosas, este archivo se puede usar para restaurar esa información a Almacén de administración central después de una actualización, un error de hardware o de cualquier otro problema que resulte en la pérdida de datos. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Export-CsConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    Export-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 exporta datos de Lync Server desde Almacén de administración central a un archivo llamado C:\\Config.zip.

    Export-CsConfiguration -FileName "C:\Config.zip"

## Descripción detallada

Los equipos que ejecutan roles de servidores o servicios de Lync Server deben tener una copia de la topología, las opciones de configuración y las directivas actuales para poder funcionar en su rol asignado. Lync Server tiene la función de garantizar que la información se transfiera a cada equipo que la necesite.

Los cmdlet **Export-CsConfiguration** y **Import-CsConfiguration** se usan para crear copias de seguridad y restaurar la topología, las opciones de configuración y las directivas de Lync Server durante la actualización de Almacén de administración central. El cmdlet **Export-CsConfiguration** permite exportar datos a un archivo .ZIP; luego, puede usar el cmdlet **Import-CsConfiguration** para leer el archivo .ZIP y restaurar la topología, las opciones de configuración y las directivas en el Almacén de administración central. Después, los servicios de replicación de Lync Server replicarán la información restaurada en otros PC que usan los servicios de Lync Server.

La capacidad de exportar e importar datos de configuración también se usa en la configuración inicial de los equipos de su red perimetral (por ejemplo, servidores perimetrales). Al configurar un equipo de la red perimetral, primero debe llevar a cabo una replicación manual con los cmdlet CsConfiguration: deberá exportar los datos de configuración con el cmdlet **Export-CsConfiguration** y después copiar el archivo .ZIP al equipo de la red perimetral. Luego, puede usar el cmdlet **Import-CsConfiguration** y el parámetro LocalStore para importar los datos. Solo será necesario hacerlo una vez; después, la replicación se ejecutará automáticamente.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a ejecutar el cmdlet **Export-CsConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsConfiguration"}

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
<td><p><em>FileName</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ruta al archivo .ZIP que se creará al ejecutar el cmdlet <strong>Export-CsConfiguration</strong>. Por ejemplo: -FileName &quot;C:\Config.zip&quot;. Recuerde que debe incluir los parámetros FileName o AsBytes, pero no ambos, al llamar al cmdlet <strong>Export-CsConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Devuelve información de topología como matriz de bytes; los datos devueltos se deben almacenar en una variable para que los pueda usar el cmdlet <strong>Import-CsConfiguration</strong>. No se pueden usar los dos parámetros AsBytes y FileName en el mismo comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error no graves que se pueden producir al iniciar el comando. Para definir el parámetro Force en True, use la sintaxis siguiente:</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración del PC local, en lugar de formar Almacén de administración central en sí.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Export-CsConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

Si se llama junto con el parámetro AsBytes, el cmdlet **Export-CsConfiguration** devuelve la información de configuración como una matriz de bytes.

## Vea también

#### Otros recursos

[Import-CsConfiguration](import-csconfiguration.md)

