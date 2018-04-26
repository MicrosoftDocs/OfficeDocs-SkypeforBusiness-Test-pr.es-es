---
title: Administrar las comunicaciones con las organizaciones y los usuarios externos
TOCTitle: Administrar las comunicaciones con las organizaciones y los usuarios externos
ms:assetid: 8a64f0fe-1e79-47d8-835e-548d7ac0757e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362813(v=OCS.15)
ms:contentKeyID: 56271305
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar las comunicaciones con las organizaciones y los usuarios externos

 

_**Última modificación del tema:** 2015-06-22_

Los siguientes cmdlets se pueden usar para administrar la federación con dominios externos y con proveedores de mensajería instantánea (MI) pública:


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
<td><p><a href="new-csedgeallowallknowndomains.md">New-CsEdgeAllowAllKnownDomains</a></p></td>
<td><p>Permite a los usuarios comunicarse con todos los dominios, excepto con los especificados en la lista de dominios bloqueados.</p>
<p>La federación es un servicio que permite a los usuarios intercambiar información de presencia y mensajería instantánea con usuarios de otros dominios. Por lo general, los administradores usan listas de dominios permitidos y bloqueados para especificar los dominios externos con lo que los usuarios se pueden comunicar.</p></td>
</tr>
<tr class="even">
<td><p><a href="new-csedgeallowlist.md">New-CsEdgeAllowList</a></p></td>
<td><p>Limita la comunicación del usuario a una colección especificada de dominios.</p>
<p>Los usuarios solo se podrán comunicar con los dominios que aparecen en la lista de dominios permitidos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="new-csedgedomainpattern.md">New-CsEdgeDomainPattern</a></p></td>
<td><p>Modifica la lista de dominios permitidos y bloqueados.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantfederationconfiguration.md">Get-CsTenantFederationConfiguration</a><br />
<a href="set-cstenantfederationconfiguration.md">Set-CsTenantFederationConfiguration</a></p></td>
<td><p>Habilita y deshabilita la federación con otros dominios y con proveedores públicos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-cstenanthybridconfiguration.md">Get-CsTenantHybridConfiguration</a><br />
<a href="set-cstenanthybridconfiguration.md">Set-CsTenantHybridConfiguration</a></p></td>
<td><p>Asigna los valores adecuados a la configuración híbrida.</p>
<p>En las implementaciones híbridas o de &quot;dominio dividido&quot;, las organizaciones tienen algunos usuarios con cuentas hospedadas en Skype Empresarial Online y, al mismo tiempo, otros con cuentas hospedadas en Lync Server 2013. De forma predeterminada, los usuarios hospedados en Skype Empresarial Online no tienen acceso a todas las funciones disponibles con Telefonía IP empresarial. Para dar a los usuarios de Skype Empresarial Online acceso a estas funciones de Telefonía IP empresarial, los administradores deben asignar los valores adecuados a la configuración híbrida. Estos valores solo se pueden administrar con los cmdlets <strong>CsTenantHybridConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantpublicprovider.md">Get-CsTenantPublicProvider</a><br />
<a href="set-cstenantpublicprovider.md">Set-CsTenantPublicProvider</a></p></td>
<td><p>Administra la federación con proveedores públicos.</p>
<p>Los proveedores públicos son organizaciones que proporcionan servicios de comunicación SIP al público en general. Cuando establece una relación de federación con un proveedor público, de hecho establece una federación con cualquier usuario que tenga una cuenta hospedada con dicho proveedor.</p></td>
</tr>
</tbody>
</table>


También puede administrar la configuración de la federación, tanto para dominios federados como para proveedores públicos, en el Centro de administración de Skype Empresarial Online:

![Configuración de la organización del centro de administración en línea de Lync](images/Dn362813.f860d03f-5906-49b0-bcc7-7634afe7005e(OCS.15).png "Configuración de la organización del centro de administración en línea de Lync")

## Vea también

#### Conceptos

[Los cmdlets de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

