---
title: New-CsConferenceDirectory
TOCTitle: New-CsConferenceDirectory
ms:assetid: fd5a4369-10cd-4337-94df-51bcaee4fde9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg413080(v=OCS.15)
ms:contentKeyID: 48277270
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferenceDirectory

 

_**Última modificación del tema:** 2015-03-09_

Crea un directorio de conferencia para su uso en la organización. Los directorios de conferencia se usan para ayudar a los usuarios de conferencia de acceso telefónico local a localizar la información de conferencias. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsConferenceDirectory -HomePool <String> -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Crea un directorio de conferencia con la identidad 42, que se hospedará en el grupo atl-cs-001.litwareinc.com.

    New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## Descripción detallada

Al crear un URI (Identificador de recursos uniforme) de conferencia de acceso telefónico local, se le asigna una dirección SIP única. Sin embargo, las direcciones SIP son difíciles de convertir para dispositivos que no sean compatibles con SIP; por ejemplo, un teléfono de red telefónica conmutada (RTC) no puede convertir una dirección SIP. Debido a esto, Lync Server usa directorios de conferencia para ayudar a estos dispositivos a localizar y conectarse a las conferencias de acceso telefónico local. Esto se lleva a cabo creando un directorio de conferencia SIP asociado con cada uno de los URI de conferencia de acceso telefónico local, y se identifica mediante un valor entero en lugar de un URI SIP. De este modo, los teléfonos de RTC y otros dispositivos pueden usar estos números (en lugar de un URI de SIP) cuando se conectan a conferencias; el número de directorio se incluye en la identificación de conferencia de RTC que especifican los usuarios cuando se conectan a una conferencia de acceso telefónico.

Para crear directorios de conferencia, llame al cmdlet **New-CsConferenceDirectory**.

Quién puede ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **New-CsConferenceDirectory** de manera local: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC), se ha asignado este cmdlet (incluidos los roles RBAC que haya creado usted mismo) para ejecutar el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferenceDirectory"}

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
<th>Requerido</th>
<th>Tipo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>HomePool</em></p></td>
<td><p>Requerido</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo de registrador donde se hospedará el nuevo directorio de conferencia. Por ejemplo: -Identity atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Requerido</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador numérico único del nuevo directorio de conferencia. Las identidades pueden ser cualquier valor entero entre 0 y 9999, ambos incluidos, pero deben ser únicas. (Por ejemplo, no puede haber dos directorios con el valor de Identity 575.) No es necesario seguir ningún orden numérico a la hora de crear directorios. Por ejemplo, puede crear un directorio con el valor de Identity 999 seguido de un directorio con el valor de Identity 2 que, a su vez, vaya seguido de un directorio con el valor de Identity 438 y así sucesivamente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan producirse al ejecutar el comando.</p></td>
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

Ninguno. El cmdlet **New-CsConferenceDirectory** no acepta canalizaciones.

## Tipos de valores devueltos

Crea nuevas instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Vea también

#### Otros recursos

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

