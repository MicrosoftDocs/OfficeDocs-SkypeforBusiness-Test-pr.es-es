---
title: Debug-CsLisConfiguration
TOCTitle: Debug-CsLisConfiguration
ms:assetid: 8cc718d6-52ec-4ff3-a77e-8d6df1725fb0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398710(v=OCS.15)
ms:contentKeyID: 48275970
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsLisConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Displays the Enhanced 9-1-1 (E9-1-1) Location Information service (LIS) configuration in XML format. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Debug-CsLisConfiguration [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Examples

## EXAMPLE 1

Running this command will display the entire LIS configuration to the Shell de administración de Lync Server window in XML format. By default, the output of the **Debug-CsLisConfiguration** cmdlet is displayed on one line, with an ellipsis (…) at the end of the line indicating that there’s more than one line of data. Therefore, in this example we pipe the output to the **Format-Table** cmdlet, specifying the Wrap parameter, to display the full output wrapped to fit in the display window.

    Debug-CsLisConfiguration | Format-Table -Wrap

## Detailed Description

The LIS configuration for an Enterprise Voice E9-1-1 implementation is stored in compressed format. This cmdlet un-compresses the configuration and displays it in XML format. This can make it quicker to debug issues with a configuration.

This cmdlet retrieves the location information from the Almacén de administración central. When this information is created, it is stored in the location database; it does not move to the Almacén de administración central until it is published with the **Publish-CsLisConfiguration** cmdlet. If the location information has not been published (or has been un-published with the **Unpublish-CsLisConfiguration** cmdlet), the **Debug-CsLisConfiguration** cmdlet will not return anything.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Debug-CsLisConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsLisConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Allows you to specify a domain controller. If no domain controller is specified, the first available will be used.</p></td>
</tr>
</tbody>
</table>


## Input Types

None.

## Return Types

Returns an object of type System.Management.Automation.PSCustomObject.

## Vea también

#### Otros recursos

[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

