---
title: Administrar directivas
TOCTitle: Administrar directivas
ms:assetid: 91372888-a96e-44db-a0dc-d08facbfce87
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362826(v=OCS.15)
ms:contentKeyID: 56271327
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar directivas

 

_**Última modificación del tema:** 2015-06-22_

Los siguientes cmdlets administran directivas de Skype Empresarial Online. Las directivas ayudan a determinar las funciones de Skype Empresarial Online que están disponibles para los usuarios y para la organización en general.


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
<td><p><a href="get-csclientpolicy.md">Get-CsClientPolicy</a><br />
<a href="grant-csclientpolicy.md">Grant-CsClientPolicy</a></p></td>
<td><p>Las directivas de cliente se usan para determinar las características del cliente Lync que están disponibles para los usuarios. Por ejemplo, puede permitir transferir archivos a algunos usuarios, pero no a otros.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csconferencingpolicy.md">Get-CsConferencingPolicy</a><br />
<a href="grant-csconferencingpolicy.md">Grant-CsConferencingPolicy</a></p></td>
<td><p>Las directivas de conferencia determinan las características y funciones que se pueden usar en una conferencia. Esto incluye cualquier cosa desde si la conferencia puede incluir audio y vídeo IP hasta el número máximo de personas que pueden asistir a una reunión.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csexternalaccesspolicy.md">Get-CsExternalAccessPolicy</a><br />
<a href="grant-csexternalaccesspolicy.md">Grant-CsExternalAccessPolicy</a></p></td>
<td><p>Las directivas de acceso externo se usan para determinar si se permite que los usuarios se comuniquen con otros usuarios de dominios federados y/o con otros usuarios que tienen cuentas en proveedores de mensajería instantánea pública, como Windows Live o AOL.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csvoicepolicy.md">Get-CsVoicePolicy</a><br />
<a href="grant-csvoicepolicy.md">Grant-CsVoicePolicy</a><br />
<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a></p></td>
<td><p>Las directivas de voz se usan para administrar características de Telefonía IP empresarial, como las llamadas simultáneas (la posibilidad de recibir una llamada en un segundo teléfono cuando alguien llama al número de la oficina) o el desvío de llamadas.</p></td>
</tr>
</tbody>
</table>


También puede administrar configuraciones de directivas de conferencia específicas en el Centro de administración de Skype Empresarial Online:

![Propiedades de opciones generales en el centro de administración de Lync](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Propiedades de opciones generales en el centro de administración de Lync")

También puede administrar configuraciones de directivas de acceso externo en el Centro de administración de Skype Empresarial Online:

![Opciones de comunicación externa en el centro de administración](images/Dn362826.e5cfb159-b096-463e-b1ef-2b42eb29168a(OCS.15).png "Opciones de comunicación externa en el centro de administración")

## Vea también

#### Conceptos

[Los cmdlets de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

