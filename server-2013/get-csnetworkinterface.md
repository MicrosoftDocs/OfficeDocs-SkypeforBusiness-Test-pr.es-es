---
title: Get-CsNetworkInterface
TOCTitle: Get-CsNetworkInterface
ms:assetid: 06a5fedf-d87e-4469-9bd6-ad16c1f9a801
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398121(v=OCS.15)
ms:contentKeyID: 48274318
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterface

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre las interfaces de red en uso en los equipos que ejecutan los servicios o los roles de servidor deLync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkInterface [-Identity <NetworkInterfaceIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterface [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ComputerFqdn <Fqdn>]

## Ejemplos

## EJEMPLO 1

El comando del ejemplo 1 devuelve información sobre todas las interfaces de red configuradas para su uso en la organización.

    Get-CsNetworkInterface

## EJEMPLO 2

El comando del ejemplo 2 devuelve información sobre una sola interfaz de red: la interfaz que tiene el parámetro Identity atl-cs-001.litwareinc.com.com/Primary/1.

    Get-CsNetworkInterface -Identity atl-cs-001.litwareinc.com/Primary/1

## EJEMPLO 3

En el ejemplo 3, se devuelve información sobre todas las interfaces de red en el dominio litwareinc.com. Para ello, se incluye el parámetro Filter junto con el valor de filtro "\*.litwareinc.com\*". Este valor de filtro limita los datos devueltos a las interfaces que tienen una identidad que incluye el valor de cadena "litwareinc.com".

    Get-CsNetworkInterface -Filter "*.litwareinc.com*"

## EJEMPLO 4

El ejemplo 4 devuelve información sobre todas las interfaces de red configuradas para la dirección IP 192.168.0.240. Para realizar esta acción, el comando primero llama al cmdlet **Get-CsNetworkInterface** sin ningún parámetro, lo que devuelve una recopilación de todas las interfaces de red configuradas para usarse en la organización. A continuación, esta recopilación se canaliza al cmdlet **Where-Object**, que selecciona solamente las interfaces en las que la propiedad IPAddress es igual a 192.168.0.240.

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -eq "192.168.0.240"}

## EJEMPLO 5

El comando que se muestra en el ejemplo 5 es una variación del comando que se muestra en el ejemplo 4; sin embargo, en este caso, se devuelve información sobre todas las interfaces de red configuradas para la subred "192.168.0.\*". Para llevar a cabo esta acción, se recupera una recopilación de todas las interfaces de red, se canaliza esa recopilación al cmdlet **Where-Object** y, luego, se seleccionan solamente las interfaces en las que IPAddress comienza con el valor de cadena "192.168.0.".

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -like "192.168.0.*"}

## EJEMPLO 6

El ejemplo 6 devuelve todas las interfaces de red que se han configurado para el acceso externo. Para ello, primero se llama al cmdlet **Get-CsNetworkInterface** sin ningún parámetro, lo que devuelve una recopilación de todas las interfaces de red actualmente en uso. A continuación, esta recopilación se canaliza al cmdlet **Where-Object**, que selecciona solamente los elementos en los que la propiedad Interface es igual a External.

    Get-CsNetworkInterface | Where-Object {$_.Interface -eq "External"}

## Descripción detallada

Para que la información se transmita de un equipo a otro, estos equipos deben contar con interfaces de red: conexiones entre el equipo y la red. Los equipos que ejecutan los servicios o los roles de servidor de Lync Server deben tener al menos una interfaz de red; de lo contrario, no podrán comunicarse con otros equipos. Sin embargo, estos equipos también pueden tener varias interfaces de red; por ejemplo, un Servidor perimetral puede tener una interfaz para conectarse a la red interna y una segunda interfaz para conectarse a Internet. El cmdlet **Get-CsNetworkInterface** les proporciona a los administradores una manera de devolver información sobre las interfaces de red que están actualmente en uso en los equipos que ejecutan los servicios o los roles de servidor de Lync Server.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Get-CsNetworkInterface** en forma local: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterface"}

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
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo del equipo para el cual se desea devolver información de la interfaz de red. Por ejemplo, a fin de devolver información de la interfaz de red para el equipo atl-cs-001.litwareinc.com (y solamente para ese equipo), use esta sintaxis: -ComputerFqdn atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite usar caracteres comodín al especificar la interfaz de red (o las interfaces) sobre la que se desea devolver información. Por ejemplo, esta sintaxis devuelve información sobre la interfaz de red principal usada en todos los equipos que ejecutan un servicio o un rol de servidor de Lync Server: -Filter &quot;*/Primary/*&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.NetworkInterfaceIdentity</p></td>
<td><p>Identificador único de la interfaz de red sobre la que se desea devolver información. Una identidad de interfaz de red consta de tres partes:</p>
<p>El nombre de dominio completo (FQDN) del equipo (por ejemplo, atl-cs-001.litwareinc.com).</p>
<p>El &quot;lado&quot; de la interfaz de red (Principal; Interna; Externa; red telefónica conmutada). El lado indica el tipo de tráfico para el que se usa el puerto.</p>
<p>El número de la interfaz de red para ese lado específico.</p>
<p>Por ejemplo: -Identity &quot;atl-cs-001.litwareinc.com/Primary/1&quot;.</p>
<p>Los parámetros Identity, ComputerFqdn y Filter deben usarse por separado; por ejemplo, no es posible ejecutar un comando que use tanto ComputerFqdn como Identity. Además, no se pueden usar caracteres comodín al especificar la identidad. Para emplear caracteres comodín, use el parámetro Filter.</p>
<p>Si no se usan los parámetros Identity, ComputerFqdn ni Filter, el cmdlet <strong>Get-CsNetworkInterface</strong> devuelve información sobre todas las interfaces de red actualmente en uso en los equipos que ejecutan un servicio o un rol de servidor de Lync Server.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsNetworkInterface** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsNetworkInterface** devuelve una instancia del objeto Microsoft.Rtc.Management.Xds.DisplayNetworkInterface.

## Vea también

#### Otros recursos

[Get-CsComputer](get-cscomputer.md)

