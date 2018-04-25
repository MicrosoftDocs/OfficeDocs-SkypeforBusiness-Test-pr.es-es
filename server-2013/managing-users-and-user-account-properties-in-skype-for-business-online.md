---
title: Administrar usuarios y propiedades de cuenta de usuario
TOCTitle: Administrar usuarios y propiedades de cuenta de usuario
ms:assetid: 5d13ab15-0e12-4bd0-a970-f130de980404
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362790(v=OCS.15)
ms:contentKeyID: 56271294
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar usuarios y propiedades de cuenta de usuario

 

_**Última modificación del tema:** 2015-06-22_

Los cmdlets siguientes sirven para administrar las cuentas de usuario de Skype Empresarial Online.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csonlineuser.md">Get-CsOnlineUser</a></p></td>
<td><p>Devuelve información sobre los usuarios que tienen cuentas hospedadas en su inquilino de Skype Empresarial Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csuseracp.md">Get-CsUserAcp</a><br />
<a href="remove-csuseracp.md">Remove-CsUserAcp</a><br />
<a href="set-csuseracp.md">Set-CsUserAcp</a></p></td>
<td><p>Permite asignar, modificar o anular la asignación de un proveedor de audioconferencia a usuarios concretos.</p>
<p>Un proveedor de audioconferencia es una compañía que ofrece servicios de conferencia a las organizaciones, incluyendo servicios de gama alta, como la traducción en directo, la transcripción y la asistencia de operador por conferencia en directo.</p>
<p>Estos cmdlets no devuelven información sobre los proveedores de audio disponibles que se pueden asignar a esos usuario. Para ver esta información, ejecute este comando:</p>
<pre><code>Get-CsAudioConferencingProvider</code></pre></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412910.warning(OCS.15).gif" title="warning" alt="warning" />Advertencia:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>El cmdlet Set-CsUser también está incluido en el conjunto de cmdlets disponible para los administradores de Skype Empresarial Online. Sin embargo, actualmente Set-CsUser no se puede usar para administrar Skype Empresarial Online, excepto para configurar el parámetro de AudioVideoDisabled. Si intenta ejecutar el cmdlet con cualquier otro parámetro, este fallará y aparecerá un mensaje de error parecido a este:<br />
No es posible configurar “SipAddress”. Este parámetro está restringido a Remote Tenant PowerShell.</td>
</tr>
</tbody>
</table>


Los proveedores de audioconferencias también se pueden asignar a cuentas de usuario (las asignaciones también se pueden anular) desde el centro de administración de Skype Empresarial Online:

![Propiedades de conferencias de marcado en el centro de administración de Lync](images/Dn362790.0c61f0c2-8aef-4020-a0a8-02580d43092a(OCS.15).png "Propiedades de conferencias de marcado en el centro de administración de Lync")

## Vea también

#### Conceptos

[Los cmdlets de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

