---
title: Get-CsUICulture
TOCTitle: Get-CsUICulture
ms:assetid: b8df7083-068b-4d5e-a9b4-448602de6586
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412900(v=OCS.15)
ms:contentKeyID: 48276464
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUICulture

 

_**Última modificación del tema:** 2015-03-09_

Returns information about the culture (that is, the language and regional settings) used by the Shell de administración de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsUICulture

## Examples

## EXAMPLE 1

The command shown in Example 1 returns basic information about the culture currently in use by the Shell de administración de Lync Server.

    Get-CsUICulture

## Detailed Description

Although Lync Server is available in multiple languages, the software is not a true MUI (multilingual user interface) application. Among other things, this means that the user interface for the Shell de administración de Lync Server does not change languages any time you change the operating system language. For example, suppose you have installed the U.S. English version of Lync Server and are also running the Windows operating system under U.S. English. If you change the operating system culture (that is, the language and regional settings) to Danish, the Shell de administración de Lync Server will not automatically follow suit; instead, the Shell de administración de Lync Server user interface (including error messages and help text) will remain in U.S. English. If you need to change the culture for the Shell de administración de Lync Server, you must run the **Set-CsUICulture** cmdlet.

The **Get-CsUICulture** cmdlet provides a way for you to determine the culture currently used in the Shell de administración de Lync Server.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Get-CsUICulture** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>This cmdlet provides only common Windows PowerShell parameters.</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Get-CsUICulture** cmdlet does not accept pipelined input.

## Return Types

The **Get-CsUICulture** cmdlet returns instances of the System.Globalization.CultureInfo class.

## Vea también

#### Otros recursos

[Set-CsUICulture](set-csuiculture.md)

