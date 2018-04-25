---
title: Set-CsConferenceServer
TOCTitle: Set-CsConferenceServer
ms:assetid: 90f9f1f1-0029-4f97-a8f4-719523cfad56
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398738(v=OCS.15)
ms:contentKeyID: 48276022
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceServer

 

_**Última modificación del tema:** 2015-03-09_

Modifica las propiedades de un Servidor de conferencia A/V (conocido también como servidor de conferencia). El servidor de conferencia ofrece funciones de audio y vídeo (A/V) para conferencias en línea. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsConferenceServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AppSharingSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-AudioVideoSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomPort <UInt16>] [-EdgeServer <String>] [-Force <SwitchParameter>] [-ImSipPort <UInt16>] [-MeetingPsomPort <UInt16>] [-PhoneSipPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 modifica el puerto SIP de mensajería instantánea del servidor de conferencia ConferencingServer:atl-cs-001.litwareinc.com. En este ejemplo, se cambia el puerto a 5075.

    Set-CsConferenceServer -Identity "ConferencingServer:atl-cs-001.litwareinc.com" -ImSipPort 5075

## Ejemplo 2

El ejemplo 2 es una variación del comando que se muestra en el ejemplo 1; pero, en este caso, el puerto SIP de mensajería instantánea se cambia en todos los servidores de conferencia de la organización. Para hacerlo, el comando usa primero el cmdlet **Get-CsService** y el parámetro ConferencingServer para devolver una colección de todos los servidores de conferencia que se usan actualmente. Después, la colección se canaliza al cmdlet **ForEach-Object**, que ejecuta el cmdlet **Set-CsConferenceServer** en cada servidor de la colección y configura el ImSipPort en 5075.

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -ImSipPort 5075}

## Descripción detallada

Los servidores de conferencia (también llamados servidores de conferencia A/V) se usan para ofrecer funciones de audio y vídeo a conferencias. A su vez, se puede usar el cmdlet **Set-CsConferenceServer** para modificar las propiedades de estos servidores; concretamente, se puede especificar qué puertos se usan para tráfico de audio, tráfico de vídeo y uso compartido de aplicaciones, por ejemplo. Se puede usar también el cmdlet **Set-CsConferenceServer** para asociar un servidor concreto con un Servidor perimetral o un Servidor de archivado.

Quién puede iniciar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a iniciar localmente el cmdlet **Set-CsConferenceServer**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Cantidad total de puertos asignados para compartir aplicaciones. Los puertos que se abrirán en la práctica comenzarán en el valor configurado en AppSharingPortStart y continuarán hasta la cantidad especificada en AppSharingPortCount. Por ejemplo, si se establece que el valor de AppSharingPortStart es 60000 y el de AppSharingPortCount es 100, se usarán los puertos del 60000 al 60099 para compartir aplicaciones.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Primer puerto del intervalo de puertos multimedia asignados para compartir aplicaciones. Por ejemplo: –AppSharingPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingSipPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto SIP usado para escuchar las peticiones de uso compartido de aplicaciones. Los puertos que se usan realmente para el uso compartido de aplicaciones se configuran con AppSharingPortStart y AppSharingPortCount.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Cantidad total de puertos asignados para enviar y recibir tráfico de audio. Los puertos que se abrirán en la práctica comenzarán en el valor configurado en AudioPortStart y continuarán hasta la cantidad especificada en AudioPortCount. Por ejemplo, si el valor de AudioPortStart es 60000 y el de AudioPortCount es 100, se usarán los puertos del 60000 al 60099 para el tráfico de audio.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Primer puerto del intervalo de puertos multimedia asignados para enviar y recibir tráfico de audio. Por ejemplo: –AudioPortStart 60000.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioVideoSipPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto SIP usado para escuchar las peticiones entrantes de servicio de audio y vídeo. Los puertos que se usan realmente para el tráfico de audio y vídeo se configuran con AudioPortCount, AudioPortStart, VideoPortCount y VideoPortStart.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto de datos que usa el protocolo Modelo de objetos compartidos persistentes (PSOM).</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Ubicación de servicio del Servidor perimetral que se debe asociar con el servidor de conferencia. Por ejemplo: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Ubicación del servicio del servidor de conferencia que se modificará. Por ejemplo: -Identity &quot;ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Tenga en cuenta que no es necesario usar el prefijo &quot;ConferencingServer:&quot; cuando se especifica un servidor de conferencia. Por ejemplo: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ImSipPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto usado para el tráfico de mensajería instantánea.</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingPsomPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto usado para el protocolo de Modelo de objetos compartidos persistentes (PSOM), un protocolo de Microsoft que se usa para las conferencias.</p></td>
</tr>
<tr class="even">
<td><p><em>PhoneSipPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto usado para el tráfico de telefonía.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Cantidad total de puertos asignados para enviar y recibir tráfico de vídeo. Los puertos que se abrirán en la práctica comenzarán en el valor configurado en VideoPortStart y continuarán hasta la cantidad especificada en VideoPortCount. Por ejemplo, si el valor de VideoPortStart es 60000 y el de VideoPortCount es 100, se usarán los puertos del 60000 al 60099 para el tráfico de vídeo.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Primer puerto del intervalo de puertos asignados para enviar y recibir tráfico de vídeo. Por ejemplo: –VideoPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Set-CsConferenceServer** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Set-CsConferenceServer** no devuelve ningún valor ni objeto. En su lugar, el cmdlet modifica las instancias existentes del objeto Microsoft.Rtc.Management.Xds.DisplayConferenceServer.

## Vea también

#### Otros recursos

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Get-CsService](get-csservice.md)

