---
title: Remove-CsConferenceDirectory
TOCTitle: Remove-CsConferenceDirectory
ms:assetid: c2c62a14-f3f3-472f-bf91-1fcea9e45425
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412961(v=OCS.15)
ms:contentKeyID: 48276592
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDirectory

 

_**Última modificación del tema:** 2015-03-09_

Quita un directorio de conferencia existente. Los directorios de conferencia se usan para ayudar a los usuarios de conferencia de acceso telefónico local a localizar información sobre las conferencias. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 elimina el directorio de conferencia con la identidad 2.

    Remove-CsConferenceDirectory -Identity 2

## Ejemplo 2

El comando anterior elimina todos los directorios de conferencia detectados en el servicio UserServer:atl-cs-001.litwareinc.com. Para ello, el comando primero llama al cmdlet **Get-CsConferenceDirectory** sin parámetros, lo que devuelve una colección de todos los directorios de conferencia que actualmente están en uso en la organización. Después, la colección se canaliza al cmdlet **Where-Object**, que solo selecciona los directorios hospedados en el servicio UserServer:atl-cs-001.litwareinc.com. A su vez, la colección filtrada se canaliza al cmdlet **Remove-CsConferenceDirectory**, que la eliminará.

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"} | Remove-CsConferenceDirectory

## Descripción detallada

Al crear un identificador de recursos uniforme (URI) de conferencia de acceso telefónico local, se le asigna una dirección SIP única. Sin embargo, las direcciones SIP son difíciles de convertir para dispositivos que no sean compatibles con SIP; por ejemplo, un teléfono de red telefónica conmutada (RTC) no puede convertir una dirección SIP. Debido a esto, Lync Server usa directorios de conferencia para ayudar a estos dispositivos a localizar y conectarse a las conferencias de acceso telefónico local. Esto se lleva a cabo creando un directorio de conferencia SIP asociado con cada uno de los URI de conferencia de acceso telefónico local, y se identifica con un valor entero en lugar de un URI SIP. Entonces, los teléfonos de RTC y otros dispositivos pueden usar estos números (en lugar de un URI de SIP) cuando se conectan a conferencias; el número de directorio se incluye en la identificación de conferencia de RTC que introducen los usuarios cuando se conectan a una conferencia de acceso telefónico.

Los directorios de conferencia se crean con el cmdlet **New-CsConferenceDirectory**. De alguna vez, puede que tenga que eliminar uno o más de estos directorios; por ejemplo, es posible que tenga que retirar el grupo de servidores donde estaban hospedados los directorios. Los directorios de conferencia se pueden retirar llamando al cmdlet **Remove-CsConferenceDirectory**. Tenga en cuenta que si necesita mover un directorio de un grupo de servidores a otro, puede hacerlo llamando al cmdlet **Move-CsConferenceDirectory**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Remove-CsConferenceDirectory** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDirectory"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identidad numérica del directorio de conferencia que se va a quitar.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, quita el directorio de conferencia, aunque el grupo de servidores que hospeda el directorio no está disponible. De forma predeterminada, el cmdlet <strong>Remove-CsConferenceDirectory</strong> no quitará ningún directorio, si no se puede contactar con el grupo de servidores correspondiente.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories. El cmdlet **Remove-CsConferenceDirectory** acepta la entrada canalizada de objetos de directorio de conferencia.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet **Removes-CsConferenceDirectory** elimina las instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Vea también

#### Otros recursos

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)

