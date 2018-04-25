---
title: Get-CsComputer
TOCTitle: Get-CsComputer
ms:assetid: 493931a9-1670-4a76-abba-7d3c7723d2e1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425959(v=OCS.15)
ms:contentKeyID: 48275177
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsComputer

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información acerca de los equipos que realizan roles de servidor en la infraestructura de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1, se usa el cmdlet **Get-CsComputer** para devolver información acerca de todos los equipos que tienen asumidos roles de servidor en la infraestructura de Lync Server.

    Get-CsComputer

## EJEMPLO 2

El comando que aparece en el ejemplo 2 usa el parámetro Filter para devolver solo aquellos equipos de roles de servidor que forman parte del dominio litwareinc.com. La cadena de caracteres comodín \*.litwareinc.com restringe la información devuelta a aquellos equipos que tienen un FQDN que acaba en el valor de cadena ".litwareinc.com".

    Get-CsComputer -Filter "*.litwareinc.com"

## EJEMPLO 3

En el ejemplo 3 se utiliza el parámetro Identity para limitar los datos devueltos al único equipo que tiene el FQDN atl-cs-001.litwareinc.com.

    Get-CsComputer -Identity "atl-cs-001.litwareinc.com"

## EJEMPLO 4

En el ejemplo 4, el parámetro Pool se usa para devolver información sobre todos los equipos detectados en el grupo atl-cs-001.litwareinc.com.

    Get-CsComputer -Pool "atl-cs-001.litwareinc.com"

## Descripción detallada

El cmdlet **Get-CsComputer** permite identificar rápidamente los equipos que ejecutan roles de servidor o servicios de Lync Server. Si se llama sin ningún parámetro, el cmdlet **Get-CsComputer** devuelve una colección con todos los equipos que ejecutan roles de servidor o servicios de Lync Server, con el parámetro Identity, el nombre del grupo y el nombre de dominio completo de cada equipo. Como alternativa, puede usar parámetros opcionales como, por ejemplo, Identity, Filter o Pool, para limitar los datos devueltos a un único equipo o a un conjunto de ellos.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Get-CsComputer** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p>Permite usar caracteres comodín al especificar la Identity del equipo o equipos que se devolverán. Por ejemplo, este comando devuelve información acerca de todos los equipos que tienen una Identity que comienza con el valor de cadena &quot;atl-&quot;: -Filter &quot;atl-*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>FQDN del equipo que se va a devolver. Por ejemplo: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Si no especifica este parámetro, se devolverán todos los equipos de Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, devuelve información únicamente para el equipo local.</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>FQDN de un grupo de Lync Server. Al utilizar este parámetro, se devolverá información acerca de todos los equipos del grupo de servidores especificado.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsComputer** no acepta canalizaciones.

## Tipos de valores devueltos

El cmdlet **Get-CsComputer** devuelve instancias del objeto Microsoft.Rtc.Management.Deploy.Internal.Machine.

## Vea también

#### Otros recursos

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

