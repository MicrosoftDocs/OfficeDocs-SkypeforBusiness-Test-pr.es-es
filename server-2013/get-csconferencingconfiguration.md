---
title: Get-CsConferencingConfiguration
TOCTitle: Get-CsConferencingConfiguration
ms:assetid: db4ab3bc-071c-4f73-a3a0-62dc8aed48a1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398965(v=OCS.15)
ms:contentKeyID: 48276896
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre la configuración de la conferencia para la organización. La configuración de conferencia determina aspectos como el tamaño máximo permitido para el contenido y los documentos de conferencia; el período de gracia del contenido (es decir, el tiempo durante el cual se almacenará el contenido antes de eliminarlo) y las direcciones URL para las descargas internas y externas del cliente admitido. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

El ejemplo 1 devuelve información sobre las opciones de configuración de conferencia que está en uso en la organización. Para ello, se llama al cmdlet **Get-CsConferencingConfiguration** sin ningún parámetro.

    Get-CsConferencingConfiguration

## Ejemplo 2

En el ejemplo 2, se devuelve la información de configuración de conferencia para el sitio de Redmond (-Identity site:Redmond). Dado que las identidades deben ser únicas, este comando siempre devolverá, como mucho, una única recopilación de opciones de configuración de conferencia.

    Get-CsConferencingConfiguration -Identity site:Redmond

## Ejemplo 3

El comando que se muestra en el ejemplo 3 devuelve información sobre todas las opciones de configuración de conferencia que se han aplicado en el ámbito del sitio. Para ello, se llama al cmdlet **Get-CsConferencingConfiguration** junto con el parámetro Filter; el valor de filtro "site:\*" garantiza que solo se devuelvan las configuraciones en las que Identity comience por el valor de cadena 'site:".

    Get-CsConferencingConfiguration -Filter "site:*"

## Ejemplo 4

El comando anterior devuelve información sobre todas las opciones de configuración de conferencia en las que no se ha establecido la organización en Litwareinc. Para completar esta tarea, el comando primero llama al cmdlet **Get-CsConferencingConfiguration** sin parámetros, lo que devuelve una colección de todas las opciones de configuración de conferencia que actualmente están en uso en la organización. La colección resultante se transfiere al cmdlet **Where-Object**, que selecciona solo las configuraciones cuya propiedad Organization no sea igual a Litwareinc.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"}

## Ejemplo 5

En el ejemplo 5, solo se devuelve información para las opciones de configuración de conferencia en las que el espacio de almacenamiento de contenido máximo sea superior a 100 megabytes. Para ello, el comando primero llama al cmdlet **Get-CsConferencingConfiguration** sin ningún parámetro para devolver una colección de todas las configuraciones de conferencia. Esta colección se canaliza al cmdlet **Where-Object**, que selecciona las configuraciones cuyo espacio de almacenamiento de contenido sea superior a 100 megabytes.

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMB -gt 100}

## Descripción detallada

Para las conferencias, la gestión y la administración se dividen en dos conjuntos de cmdlets. Para gestionar qué tipo de actividades pueden realizar los usuarios (por ejemplo, si los usuarios pueden invitar a participantes anónimos a unirse a una conferencia, si pueden ofrecer en una conferencia compartir aplicaciones o si pueden transferir archivos en una conferencia, etc.), se utilizan los cmdlets **CsConferencingPolicy**.

Además de las actividades de usuario, los administradores deben gestionar el Lync Server Servicio de conferencia web. Por ejemplo, los administradores deben poder especificar la cantidad máxima de almacenamiento de contenido asignada a una sola conferencia, así como el período de gracia previo a la eliminación automática del contenido de la conferencia. Asimismo, deben poder especificar los puertos usados para actividades como el uso compartido de aplicaciones y la transferencia de archivos.

Estas últimas actividades se pueden gestionar utilizando los cmdlets **CsConferencingConfiguration**. Estos cmdlets permiten gestionar los servidores propiamente dichos. Los cmdlets **CsConferencingConfiguration** (que se pueden aplicar al ámbito global, de sitio o de servicio) no se usan para especificar si un usuario puede compartir aplicaciones o no durante una conferencia; no obstante, si se permite compartir aplicaciones, estos cmdlets permiten indicar qué puertos se deberían usar para hacerlo. Asimismo, los cmdlets permiten especificar aspectos como los límites de almacenamiento y los períodos de expiración, así como punteros a direcciones URL internas y externas, donde los usuarios pueden obtener recursos y ayuda sobre conferencias.

El cmdlet **Get-CsConferencingConfiguration** permite a los administradores devolver información sobre todas las configuraciones de conferencia que están en uso en su organización.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Get-CsConferencingConfiguration**: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingConfiguration"}

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
<td><p>Le permite usar comodines al especificar la identidad de las opciones de configuración de conferencia que se deben devolver. Por ejemplo, esta sintaxis devuelve todas las opciones configuradas en el ámbito del sitio: -Filter &quot;site:*&quot;. Esta sintaxis devuelve todas las opciones configuradas en el ámbito del servicio: -Filter &quot;service:*&quot;.</p>
<p>Tenga en cuenta que no es posible usar los parámetros Identity y Filter en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único de la recopilación de opciones de configuración de conferencia que se va a recuperar. Para recuperar la configuración global, use esta sintaxis: -Identity global. Para recuperar las opciones configuradas en el ámbito de sitio, use una sintaxis similar a esta: -Identity &quot;site:Redmond&quot;. Para recuperar las opciones configuradas en el ámbito de servicio, use una sintaxis similar a esta: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Si no se incluye este parámetro, el cmdlet <strong>Get-CsConferencingConfiguration</strong> devolverá toda las opciones de configuración de conferencia que esté en uso en la organización.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración de conferencia de la réplica local del Almacén de administración central en lugar de recuperarlos del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsConferencingConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsConferencingConfiguration** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Vea también

#### Otros recursos

[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

