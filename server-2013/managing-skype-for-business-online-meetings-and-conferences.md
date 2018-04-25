---
title: Administrar conferencias y reuniones de Lync Online
TOCTitle: Administrar conferencias y reuniones de Lync Online
ms:assetid: a4d0c070-4df2-47df-a1e2-6ce62600a287
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362833(v=OCS.15)
ms:contentKeyID: 56271340
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar conferencias y reuniones de Lync Online

 

_**Última modificación del tema:** 2015-06-22_

Los siguientes cmdlets se pueden usar para administrar la configuración de reuniones y conferencias:


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
<td><p><a href="disable-csmeetingroom.md">Disable-CsMeetingRoom</a><br />
<a href="enable-csmeetingroom.md">Enable-CsMeetingRoom</a><br />
<a href="get-csmeetingroom.md">Get-CsMeetingRoom</a><br />
<a href="set-csmeetingroom.md">Set-CsMeetingRoom</a></p></td>
<td><p>Administra dispositivos de extremo para salas de reuniones.</p>
<p>En Skype Empresarial Online, las salas de reuniones son aplicaciones informáticas autocontenidas que se instalan en salas de conferencias y proporcionan funciones avanzadas de reuniones. Para administrar estos nuevos dispositivos de extremo deberá, entre otras cosas, crear y habilitar una cuenta de buzón de recursos de Exchange para el dispositivo y luego habilitarla para Skype Empresarial Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csaudioconferencingprovider.md">Get-CsAudioConferencingProvider</a></p></td>
<td><p>Devuelve información sobre los proveedores de audioconferencia que tienen contrato con su organización.</p>
<p>Un proveedor de audioconferencia es una compañía de terceros que proporciona servicios de conferencia a las organizaciones, incluidos servicios de alta gama, como traducción en directo, transcripción y asistencia de operador por conferencia en directo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a><br />
<a href="set-csmeetingconfiguration.md">Set-CsMeetingConfiguration</a></p></td>
<td><p>Controla el tipo de reuniones que pueden crear los usuarios y determina cómo participan en las reuniones los usuarios de conferencias anónimos o de acceso telefónico local.</p>
<p>Las reuniones (también llamadas “conferencias”) son una parte integral de Skype Empresarial Online. Con estos cmdlets, por ejemplo, puede configurar las reuniones de modo que los usuarios de acceso telefónico local no se admitan automáticamente en la reunión, sino que se enruten a la sala de espera de esta. Estos usuarios de acceso telefónico local permanecerán en la sala de espera hasta que un moderador los admita en la reunión.</p></td>
</tr>
</tbody>
</table>


También puede administrar un subconjunto más pequeño de propiedades de configuración de reuniones en el Centro de administración de Skype Empresarial Online:

![Propiedades de opciones generales en el centro de administración de Lync](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Propiedades de opciones generales en el centro de administración de Lync")

## Vea también

#### Conceptos

[Los cmdlets de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

