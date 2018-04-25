---
title: Get-CsPool
TOCTitle: Get-CsPool
ms:assetid: e0911c68-9a0a-461a-88d6-c610c6cd996c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398992(v=OCS.15)
ms:contentKeyID: 48276914
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPool

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los grupos usados en la implementación de Lync Server. Los grupos son una colección de equipos de un sitio que ejecutan el mismo conjunto de servicios de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Site <String>]

## Ejemplos

## Ejemplo 1

El comando anterior devuelve todos los grupos encontrados en la implementación de Lync Server.

    Get-CsPool

## Ejemplo 2

En el ejemplo 2 se muestra información detallada sobre los equipos de cada grupo. Para ello, se llama al cmdlet **Get-CsPool** y luego se canalizan los datos devueltos al cmdlet **Select-Object**. El parámetro ExpandProperty de Select-Object se utiliza entonces para expandir el valor de la propiedad Computers. La propiedad Computers es una matriz de objetos que representan a cada equipo del grupo. Cuando se expande la propiedad Computers, se obtiene información detallada sobre cada uno de estos equipos.

    Get-CsPool | Select-Object -ExpandProperty Computers

## Ejemplo 3

En el ejemplo anterior, se utiliza el parámetro Identity para limitar los datos devueltos al grupo que tenga Identity atl-cs-001.litwareinc.com.

    Get-CsPool -Identity atl-cs-001.litwareinc.com

## Ejemplo 4

El Ejemplo 4 devuelve todos los grupos del sitio de Redmond. Para ello, el comando usa el parámetro Site; el valor de parámetro "Redmond" limita los datos devueltos a los grupos cuya propiedad Site sea igual a Redmond.

    Get-CsPool -Site "Redmond"

## Ejemplo 5

El comando mostrado en el ejemplo 5 devuelve una colección de todos los grupos que no tengan instalados los servicios de Lync Server. Para llevar a cabo esta tarea, el comando primero llama al cmdlet **Get-CsPool** sin ningún parámetro, lo que devuelve una colección de todos los grupos que están en uso en la organización. Esta colección se canaliza al cmdlet **Where-Object**, que selecciona todos los grupos donde la propiedad Services.Count sea igual a 0. Si Count es igual a 0, significa que no hay servicios de Lync Server configurados para dicho grupo.

    Get-CsPool | Where-Object {$_.Services.Count -eq 0}

## Descripción detallada

En Lync Server, un grupo está formado por uno o más equipos localizados en el mismo sitio y que ejecutan el mismo conjunto de servicios. Por ejemplo, si tiene un servidor que ejecuta el servicio de Servidor de mediación en el sitio de Redmond, tiene un grupo de Servidor de mediación compuesto por un solo equipo. Si tiene dos equipos que ejecutan el Servidor de mediación en el sitio de Redmond, tiene un grupo de Servidor de mediación compuesto por dos equipos. El número de grupos que se usan en la organización depende del número de servidores que tenga y de los diferentes servicios que ejecuten dichos servidores.

El cmdlet **Get-CsPool** le permite recuperar información sobre cada grupo que esté en uso en la organización, incluida la información sobre los servicios que se ejecutan en cada uno de los grupos.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Get-CsPool**: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPool"}

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
<td><p>Permite usar caracteres comodín para especificar la identidad del grupo o los grupos que se van a devolver. Por ejemplo, esta sintaxis devuelve todos los grupos que tengan una identidad que termine con el valor de cadena de caracteres &quot;.fabrikam.com&quot;: -Filter &quot;*.fabrikam.com&quot;.</p>
<p>Tenga en cuenta que no se pueden utilizar ambos parámetros, Filter e Identity, en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo de servidores que se devolverá. Por ejemplo: -Identity atl-cs-001.litwareinc.com.</p>
<p>Si este parámetro no está presente, se devolverán todos los grupos de la organización.</p></td>
</tr>
<tr class="odd">
<td><p><em>Site</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Devuelve todos los grupos del sitio especificado. Debe hacerse referencia al sitio en cuestión usando el nombre para mostrar (DisplayName) del sitio (por ejemplo, Redmond) en lugar de la identidad (Identity) (por ejemplo, site:Redmond). Por ejemplo: -Site &quot;Redmond&quot;. Puede recuperar los nombres para mostrar de sus sitios mediante la ejecución de este comando:</p>
<p>Get-CsSite | Select-Object Identity, DisplayName</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsPool** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsPool** devuelve instancias del objeto Microsoft.Rtc.Management.Deploy.Internal.Cluster.

## Vea también

#### Otros recursos

[Get-CsSite](get-cssite.md)  
[Get-CsTopology](get-cstopology.md)

