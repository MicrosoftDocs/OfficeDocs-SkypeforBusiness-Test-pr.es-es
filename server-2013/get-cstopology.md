---
title: Get-CsTopology
TOCTitle: Get-CsTopology
ms:assetid: ad52f545-b8dd-411e-8584-b6e29fe8ef18
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412824(v=OCS.15)
ms:contentKeyID: 48276346
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTopology

 

_**Última modificación del tema:** 2015-03-09_

Returns information about your Lync Server infrastructure, including internal domains, sites, clusters, computers, services, and back-end instances of SQL Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsTopology [-AsXml <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Examples

## EXAMPLE 1

Example 1 returns complete details for your Lync Server topology. This is done by calling the **Get-CsTopology** cmdlet without any additional parameters.

    Get-CsTopology

## EXAMPLE 2

Example 2 returns information about the computers found in your Lync Server topology. To do this, the command first calls the **Get-CsTopology** cmdlet to return the complete Lync Server topology. This information is then piped to the **Select-Object** cmdlet, which uses the ExpandProperty parameter to extract and display detailed information for all the computers included in that topology.

    Get-CsTopology | Select-Object -ExpandProperty Machines

## EXAMPLE 3

The command shown in Example 3 returns information about your Lync Server topology and then saves that information to an XML file. To carry out this task, the command first calls the **Get-CsTopology** cmdlet, along with the AsXml parameter; that causes the data to be returned as formatted XML. That formatted data is then piped to the **Out-File** cmdlet, which saves the information to the file C:\\Logs\\Topology.xml.

    Get-CsTopology -AsXML | Out-File C:\Logs\Topology.xml

## Detailed Description

The **Get-CsTopology** cmdlet returns information about how Lync Server has been set up and configured. Called without any additional parameters, the cmdlet provides an overview of your Lync Server infrastructure; in that scenario, the cmdlet gives you an overall view of such things as your domains, your sites, and the computers running Lync Server services and server roles. Alternatively, you can pass the output of the **Get-CsTopology** cmdlet to the **Select-Object** cmdlet; this enables you to access detailed information about a portion of your topology. For example, the following command provides detailed information regarding the SQL Server instances used by Lync Server:

Get-CsTopology | Select-Object –ExpandProperty SqlInstances

You can also use the AsXml parameter to return detailed information about your entire topology in XML format.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Get-CsTopology** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins.

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
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AsXml</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Returns topology information in XML format. By combining the <strong>Get-CsTopology</strong> cmdlet, the AsXml parameter, and the <strong>Out-File</strong> cmdlet, you can export your topology to an XML file.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Retrieves the topology data from the local replica of the Almacén de administración central rather than from the Almacén de administración central itself.</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Get-CsTopology** cmdlet does not accept pipelined input.

## Return Types

The **Get-CsTopology** cmdlet returns instances of the Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology object.

## Vea también

#### Otros recursos

[Enable-CsTopology](enable-cstopology.md)  
[Publish-CsTopology](publish-cstopology.md)  
[Test-CsTopology](test-cstopology.md)

