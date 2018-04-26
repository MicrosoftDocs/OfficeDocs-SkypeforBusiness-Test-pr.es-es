---
title: Get-CsHostedVoicemailPolicy
TOCTitle: Get-CsHostedVoicemailPolicy
ms:assetid: 52dd4397-b1c5-44a5-a744-75d715a4511b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398348(v=OCS.15)
ms:contentKeyID: 48275240
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHostedVoicemailPolicy

 

_**Última modificación del tema:** 2015-03-09_

Retrieves a hosted voice mail policy. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsHostedVoicemailPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsHostedVoicemailPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Examples

## EXAMPLE 1

This command returns all defined hosted voice mail policies for the Lync Server implementation.

    Get-CsHostedVoicemailPolicy

## EXAMPLE 2

This command returns the policy settings for the per-user hosted voice mail policy ExRedmond.

    Get-CsHostedVoicemailPolicy -Identity ExRedmond

## EXAMPLE 3

This command returns the policy settings for all per-user hosted voice mail policies (policies beginning with the tag scope).

    Get-CsHostedVoicemailPolicy -Filter tag:*

## EXAMPLE 4

This command returns the hosted voice mail policy for the Lync Online tenant with the tenant ID 73d355dd-ce5d-4ab9-bf49-7b822c18dd98.

    Get-CsHostedVoicemailPolicy -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98"

## Detailed Description

This cmdlet retrieves a policy that specifies how to route unanswered calls to a user to a hosted Mensajería unificada de Exchange (UM) service.

A user must be enabled for Mensajería unificada de Exchange hosted voice mail for this policy to take effect. You can call the **Get-CsUser** cmdlet and check the HostedVoiceMail property to determine whether a user is enabled for hosted voice mail. (A value of True means the user is enabled.)

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Get-CsHostedVoicemailPolicy** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHostedVoicemailPolicy"}

``` 
```

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
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>This parameter allows you to do a wildcard search on the Identity of the hosted voice mail policy. This will retrieve all instances of a hosted voice mail policy where the Identity matches the wildcard pattern specified in the Filter value.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>The unique identifier for the hosted voice mail policy you want to retrieve. The Identity includes the scope (in the case of global), the scope and site (for a site policy, such as site:Redmond), or the policy name (for a per-user policy, such as HVUserPolicy).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Retrieves the hosted voice mail policy from the local replica of the Almacén de administración central, rather than the Almacén de administración central itself.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>Globally unique identifier (GUID) of the Skype Empresarial Online tenant account whose voicemail policy is to be retrieved.</p>
<p>For example:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>You can return the tenant ID for each of your tenants by running this command:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>If you are using a remote session of Windows PowerShell and are connected only to Skype Empresarial Online you do not have to include the Tenant parameter. Instead, the tenant ID will automatically be filled in for you based on your connection information. The Tenant parameter is primarily for use in a hybrid deployment.</p></td>
</tr>
</tbody>
</table>


## Input Types

None.

## Return Types

This cmdlet returns an object of type Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy

## Vea también

#### Otros recursos

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

