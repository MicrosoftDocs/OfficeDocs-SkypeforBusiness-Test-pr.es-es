---
title: Administrar el correo de voz hospedado y la mensajería unificada de Exchange
TOCTitle: Administrar el correo de voz hospedado y la mensajería unificada de Exchange
ms:assetid: 844bf8d5-e093-4dcd-abcf-48dc70e8c73c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362822(v=OCS.15)
ms:contentKeyID: 56271314
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar el correo de voz hospedado y la mensajería unificada de Exchange

 

_**Última modificación del tema:** 2015-06-22_

Los cmdlets siguientes se pueden usar para administrar Mensajería unificada (UM) de Exchange y las directivas de correo de voz hospedadas:


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
<td><p><a href="get-csexumcontact.md">Get-CsExUmContact</a></p>
<p><a href="new-csexumcontact.md">New-CsExUmContact</a></p>
<p><a href="remove-csexumcontact.md">Remove-CsExUmContact</a></p>
<p><a href="set-csexumcontact.md">Set-CsExUmContact</a></p></td>
<td><p>Crea y administra objetos contacto usados para los servicios Operador automático y Acceso de suscriptor cuando Mensajería unificada (UM) de Exchange es un servicio hospedado.</p>
<p>Skype Empresarial Online colabora con Mensajería unificada (UM) de Exchange para ofrecer varias capacidades relacionadas con la voz, como el Operador automático y el Acceso de suscriptor. Operador automático permite que las llamadas se respondan automáticamente y se redirijan a la persona correspondiente. Acceso de suscriptor permite a los usuarios conectarse a Mensajería unificada (UM) de Exchange y recuperar correos, mensajes de voz, contactos e información del calendario.</p>
<p>Cuando Mensajería unificada (UM) de Exchange se ofrece como servicio hospedado, los objetos contacto usados para los servicios Operador automático y Acceso de suscriptor se deben crear usando Windows PowerShell. Estos objetos se crean y administran con los cmdlets CsExUmContact.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cshostedvoicemailpolicy.md">Get-CsHostedVoicemailPolicy</a></p>
<p><a href="grant-cshostedvoicemailpolicy.md">Grant-CsHostedVoicemailPolicy</a></p></td>
<td><p>Administra las directivas de correo de voz hospedado que se usan en la organización. Las directivas de correo de voz hospedado determinan la forma en que las llamadas no respondidas se redirigen al servicio Mensajería unificada (UM) de Exchange. Estas directivas solo afectan a los usuarios que se han habilitado para el correo de voz hospedado de Mensajería unificada (UM) de Exchange. Para comprobar si un usuario está habilitado para el correo de voz hospedado, ejecute un comando parecido a este desde el símbolo del sistema de Windows PowerShell:</p>
<pre><code>Get-CsOnlineUser -Identity &quot;kenmyer@litwareinc.com&quot; | Select-Object HostedVoiceMail</code></pre></td>
</tr>
</tbody>
</table>


La configuración de Mensajería unificada (UM) de Exchange y las directivas de correo de voz hospedado no se pueden administrar desde el centro de administración de Skype Empresarial Online.

## Vea también

#### Conceptos

[Los cmdlets de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

