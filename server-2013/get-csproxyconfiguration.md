---
title: Get-CsProxyConfiguration
TOCTitle: Get-CsProxyConfiguration
ms:assetid: e4836619-026f-4df0-adbd-aa5216e36368
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399011(v=OCS.15)
ms:contentKeyID: 48276959
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsProxyConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre las opciones de configuración de servidor proxy definidas en la organización. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsProxyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve una colección de todas las opciones de configuración de proxy en uso en la organización. Para ello, se llama al cmdlet **Get-CsProxyConfiguration** sin parámetros.

    Get-CsProxyConfiguration

## Ejemplo 2

En el ejemplo 2, se devuelve información sobre las opciones de configuración de proxy que tienen la identidad service:EdgeServer:atl-cs-001.litwareinc.com. Como las identidades deben ser únicas, este comando nunca devolverá más de una colección de configuraciones.

    Get-CsProxyConfiguration -Identity "service:EdgeServer:atl-cs-001.litwareinc.com"

## Ejemplo 3

El comando anterior devuelve información sobre todas las configuraciones de proxy configuradas en el ámbito de servicio. Para ello, el comando llama al cmdlet **Get-CsProxyConfiguration** con el parámetro Filter; el valor de filtro "service:\*" garantiza que solo se devolverán las configuraciones con una identidad que comience por la cadena "service:".

    Get-CsProxyConfiguration -Filter "service:*"

## Ejemplo 4

El ejemplo 4 devuelve información sobre las opciones de configuración de proxy que no permiten el uso de certificados de cliente como mecanismo de autenticación. Para ello, el comando primero usa el cmdlet **Get-CsProxyConfiguration** para devolver una colección de todas las opciones de configuración de proxy en uso. Esta colección se canaliza al cmdlet **Where-Object**, que selecciona solamente las configuraciones en las que la propiedad UseCertificateForClientToProxyAuth es igual a False.

    Get-CsProxyConfiguration | Where-Object {$_.UseCertificateForClientToProxyAuth -eq $False}

## Ejemplo 5

El comando anterior devuelve todas las opciones de configuración de proxy en las que el tamaño máximo del cuerpo de mensajes de clientes es menor que 5000 kilobytes. Para ello, el comando primero llama al cmdlet **Get-CsProxyConfiguration** sin parámetros, lo que devuelve una colección de todas las configuraciones de proxy en uso. La colección se canaliza al cmdlet **Where-Object**, que selecciona las configuraciones en las que la propiedad MaxClientMessageBodySizeKb es menor que 5000 días.

    Get-CsProxyConfiguration | Where-Object {$_.MaxClientMessageBodySizeKb -lt 5000}

## Descripción detallada

Lync Server permite administrar los servidores proxy mediante las opciones de configuración de servidor proxy. Estas opciones de configuración, que pueden aplicarse en el ámbito global y en el ámbito de servicio (aunque solo para los servicios del Servidor perimetral y de registrador) permiten controlar aspectos tales como los protocolos de autenticación que pueden usarse en los extremos cliente, y si se usará o no la compresión en las conexiones entrantes y salientes de servidor proxy. Al instalar Lync Server, se crea una colección global de opciones de configuración de servidor proxy automáticamente. También puede crear recopilaciones adicionales en el ámbito de servicio.

El cmdlet **Get-CsProxyConfiguration** permite devolver información sobre cualquiera de las configuraciones de servidor proxy de la organización.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Get-CsProxyConfiguration**: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsProxyConfiguration"}

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
<td><p>Permite usar caracteres comodín al especificar las opciones de configuración proxy que se devolverán. Por ejemplo, usando esta sintaxis se devuelven todas las configuraciones del ámbito de servicio: -Filter &quot;service:*&quot;.</p>
<p>No se pueden usar los parámetros –Identity y –Filter en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único de las opciones de configuración de servidor proxy que se devolverán. Para devolver la configuración global, use esta sintaxis: -Identity global. Para devolver la configuración definida en el ámbito de servicio, use una sintaxis similar a esta: -Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;. Tenga en cuenta que no puede usar caracteres comodín para especificar una identidad. Si necesita usar caracteres comodín, use el parámetro Filter.</p>
<p>Si no incluye este parámetro, el cmdlet <strong>Get-CsProxyConfiguration</strong> devuelve todas las configuraciones de servidor de proxy de la organización.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración de proxy de la réplica local del Almacén de administración central en lugar de recuperarlos del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsProxyConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsProxyConfiguration** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings.

## Vea también

#### Otros recursos

[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

