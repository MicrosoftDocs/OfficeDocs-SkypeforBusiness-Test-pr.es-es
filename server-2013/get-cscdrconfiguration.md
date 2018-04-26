---
title: Get-CsCdrConfiguration
TOCTitle: Get-CsCdrConfiguration
ms:assetid: 4af8ffa2-63d3-4873-8dac-5afede090d4f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398298(v=OCS.15)
ms:contentKeyID: 48275155
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCdrConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información acerca de la configuración de registro de detalles de llamada (CDR). CDR le permite realizar el seguimiento del uso de elementos como las sesiones de mensajería de voz punto a punto, las llamadas telefónicas de voz sobre IP (VoIP) y las llamadas en conferencia. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCdrConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

En este ejemplo se usa el cmdlet **Get-CsCdrConfiguration** para devolver una colección con todas las configuraciones de CDR que se han establecido para su uso en la organización.

    Get-CsCdrConfiguration

## EJEMPLO 2

El Ejemplo 2 usa el parámetro Identity para devolver una única recopilación de configuraciones de CDR: la configuración con el parámetro Identity site:Redmond.

    Get-CsCdrConfiguration -Identity site:Redmond

## EJEMPLO 3

En el ejemplo 3, se usa el parámetro Filter para devolver todas las configuraciones de CDR que se hayan configurado en el ámbito del sitio. El valor del filtro "site:\*" devuelve todas las configuraciones de CDR que tienen una Identidad que comienza con el valor de cadena "site:" Por definición, esas configuraciones son las que se realizaron en el ámbito del sitio.

    Get-CsCdrConfiguration -Filter site:*

## EJEMPLO 4

En el ejemplo 4 se devuelve una colección con todas las configuraciones de CDR cuya propiedad KeepCallDetailForDays es menor que 30 días. En primer lugar, el comando usa el cmdlet **Get-CsCdrConfiguration** para devolver una colección con todas las configuraciones de CDR que se han establecido en la organización. A continuación, esta colección se canaliza al cmdlet **Where-Object**, que selecciona solo aquellas configuraciones cuyo valor de KeepCallDetailForDays es menor que 30 días.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30}

## Descripción detallada

El registro de detalles de llamadas (CDR) brinda una manera de realizar el seguimiento del uso de funciones de Lync Server, como llamadas telefónicas de voz sobre IP, mensajería instantánea (MI), transferencias de archivos, conferencias de audio/vídeo (A/V) y sesiones de uso compartido de aplicaciones. CDR (que está disponible solamente si ha implementado el servicio de supervisión) mantiene la información de uso: registra información, por ejemplo, los participantes de la llamada, la duración de la llamada y la posibilidad de que se haya llevado a cabo la transferencia de archivos. (Sin embargo, CDR no registra la llamada en sí).

CDR, además, mantiene un seguimiento de los errores de la llamada: datos de diagnóstico detallados de sesiones punto a punto y para llamadas en conferencia.

Como administrador, puede determinar si se usa CDR en su organización. En caso de que se haya implementado el servicio de supervisión, puede habilitar o deshabilitar CDR. Además, puede tomar esta decisión de manera global (en cuyo caso CDR se habilitará o se deshabilitará en toda la organización) o sitio por sitio; por ejemplo, puede usar CDR en Redmond site, pero en Paris site.

El cmdlet **Get-CsCdrConfiguration** brinda una manera que le permite devolver información detallada acerca de cómo se usa CDR en su organización.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar el cmdlet **Get-CsCdrConfiguration** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCdrConfiguration"}

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
<td><p>Permite que use caracteres comodines para devolver una recopilación de configuraciones de CDR. Por ejemplo, para devolver una recopilación de todas las configuraciones definidas en el ámbito del sitio, use la sintaxis: -Filter site:*. Para devolver una recopilación de todas las configuraciones que tienen el valor de cadena &quot;Western&quot; en alguna parte del parámetro Identity, use esta sintaxis: -Filter *Western*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica el único identificador para la recopilación de la configuración de CDR que desea devolver. Para hacer referencia a la configuración global, use la siguiente sintaxis: -Identity global. Para hacer referencia a una recopilación configurada en el ámbito del sitio, use una sintaxis similar a la siguiente: -Identity site:Redmond. Tenga en cuenta que no es posible usar comodines al especificar un parámetro Identity. Si necesita usar caracteres comodín, use el parámetro Filter.</p>
<p>Si no se especifica este parámetro, el cmdlet <strong>Get-CsCdrConfiguration</strong> devuelve una colección con todos los valores de configuración de CDR que actualmente se encuentran en uso en la organización.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración de CDR de la réplica local de Almacén de administración central, en lugar de Almacén de administración central en sí.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsCdrConfiguration** no acepta canalizaciones.

## Tipos de valores devueltos

El cmdlet **Get-CsCdrConfiguration** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Vea también

#### Otros recursos

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

