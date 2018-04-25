---
title: Remove-CsConferencingConfiguration
TOCTitle: Remove-CsConferencingConfiguration
ms:assetid: a3dff4b0-100b-46fa-9078-d3b0d4914d87
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412767(v=OCS.15)
ms:contentKeyID: 48276184
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Quita la colección especificada de opciones de configuración de conferencia. La configuración de conferencia determina, por ejemplo, el tamaño máximo permitido para el contenido y los documentos de conferencias, el período de gracia del contenido y las direcciones URL para descargas internas y externas del cliente admitido. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando anterior elimina las configuraciones de conferencias aplicadas al sitio Redmond. Cuando se eliminan configuraciones como estas, los usuarios del sitio heredarán automáticamente las configuraciones globales para conferencias.

    Remove-CsConferencingConfiguration -Identity site:Redmond

## Ejemplo 2

En el ejemplo 2, el comando elimina todas las configuraciones de conferencias aplicadas en el ámbito de sitio. Para ello, el comando llama primero al cmdlet **Get-CsConferencingConfiguration** con el parámetro Filter; el valor de filtro "site:" garantiza que solo se devolverán las configuraciones cuya identidad comience con los caracteres "site:". Después, la colección filtrada se canaliza al cmdlet **Remove-CsConferencingConfiguration**, que elimina cada elemento de la colección.

    Get-CsConferencingConfiguration -Filter site:* | Remove-CsConferencingConfiguration

## Ejemplo 3

En el ejemplo 3, se eliminan todas las configuraciones de conferencia donde la organización no sea Litwareinc. Para ello, el comando llama primero al cmdlet **Get-CsConferencingConfiguration** sin ningún parámetro; esta acción devuelve una colección de todas las opciones de configuración de conferencia que se usan en la organización. Después, esta colección se canaliza al cmdlet **Where-Object**, que selecciona únicamente las configuraciones en las que la propiedad Organization sea distinta de Litwareinc. Por último, la colección filtrada se canaliza al cmdlet **Remove-CsConferencingConfiguration**, que elimina todas las configuraciones de la colección.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"} | Remove-CsConferencingConfiguration

## Descripción detallada

Para las conferencias, la gestión y la administración se dividen en dos conjuntos de cmdlets. Para administrar qué tipo de actividades pueden hacer los usuarios (por ejemplo, si los usuarios pueden invitar a participantes anónimos a unirse a una conferencia, si pueden ofrecer en una conferencia compartir aplicaciones, si pueden transferir archivos en una conferencia, etc.), se utilizan los cmdlets **CsConferencingPolicy**.

Además de las actividades de usuario, los administradores deben administrar el Servicio de conferencia web. Por ejemplo, los administradores deben poder especificar la cantidad máxima de almacenamiento de contenido asignada a una sola conferencia, así como especificar el período de gracia previo a la eliminación automática del contenido de la conferencia. También tienen que ser capaces de especificar los puertos utilizados, por ejemplo, para compartir aplicaciones y transferir archivos.

Estas últimas actividades se pueden administrar con los cmdlets **CsConferencingConfiguration**. Estos cmdlets permiten administrar los servidores reales. Los cmdlets **CsConferencingConfiguration** (que se pueden aplicar al ámbito global, de sitio o de servicio) no se usan para especificar si un usuario puede compartir aplicaciones o no durante una conferencia; no obstante, si se permite compartir aplicaciones, estos cmdlets permiten indicar qué puertos se deberían usar para hacerlo. Asimismo, los cmdlets permiten especificar aspectos como los límites de almacenamiento y los períodos de expiración, así como punteros a direcciones URL internas y externas, donde los usuarios pueden obtener recursos y ayuda sobre conferencias.

El cmdlet **Remove-CsConferencingConfiguration** proporciona un modo de eliminar cualquier colección personalizada de configuraciones de conferencias que se haya creado para uso en la organización. Cuando se elimina una colección de configuraciones, los servidores afectados por esas configuraciones pasarán a depender automáticamente de la siguiente colección en la jerarquía (servicio – sitio - global). Si las configuraciones eliminadas se aplican en el ámbito de servicio, los servidores serán administrados por las configuraciones del sitio. Si no hay configuraciones en el ámbito de sitio, los servidores pasarán a administrarse con las configuraciones globales. Del mismo modo, si elimina configuraciones en el ámbito de sitio, los servidores administrados anteriormente por dichas configuraciones pasarán a administrarse por las configuraciones globales.

Tenga en cuenta que también puede ejecutar el cmdlet **Remove-CsConferencingConfiguration** para la configuración global. Sin embargo, en ese caso no se quitará la configuración global; Lync Server no permite quitar una configuración global. En su lugar, se restablecerán los valores predeterminados de todas las propiedades de la colección global. Por ejemplo, si antes había cambiado el valor máximo de almacenamiento de contenido a 200 MB, esta propiedad se revertirá al valor predeterminado, que es 100 MB.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Remove-CsConferencingConfiguration** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingConfiguration"}

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
<td><p>Identificador único para la colección de configuraciones de conferencia que se debe quitar. Para quitar la configuración definida en el ámbito de sitio, use la sintaxis del siguiente ejemplo: -Identity &quot;site:Redmond&quot;. Para quitar la configuración definida en el ámbito de servicio, use la sintaxis del siguiente ejemplo: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>El cmdlet <strong>Remove-CsConferencingConfiguration</strong> se puede ejecutar también para la configuración global. Pero, si lo hace, esa configuración no se quitará, sino que simplemente se restablecerán los valores predeterminados de todas las propiedades.</p></td>
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
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings. El cmdlet **Remove-CsConferencingConfiguration** acepta instancias canalizadas del objeto de configuración de conferencia.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet **Remove-CsConferencingConfiguration** elimina instancias existentes del objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Vea también

#### Otros recursos

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

