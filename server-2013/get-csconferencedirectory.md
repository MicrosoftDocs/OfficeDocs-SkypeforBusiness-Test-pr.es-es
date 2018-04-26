---
title: Get-CsConferenceDirectory
TOCTitle: Get-CsConferenceDirectory
ms:assetid: 2b7927ab-c6b3-42ce-9c27-9825cd47fd77
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425771(v=OCS.15)
ms:contentKeyID: 48274775
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDirectory

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los directorios de conferencia configurados en su organización. Los directorios de conferencia se usan para ayudar a los usuarios de conferencia de acceso telefónico local a localizar la información de conferencias. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsConferenceDirectory [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDirectory [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 devuelve información sobre todos los directorios de conferencia configurados en su organización.

    Get-CsConferenceDirectory

## EJEMPLO 2

El Ejemplo 2 devuelve información sobre el directorio de conferencia con la identidad 2. Debido a que las identidades deben ser únicas, este comando nunca devolverá más de un único directorio de conferencia.

    Get-CsConferenceDirectory -Identity 2

## EJEMPLO 3

En el ejemplo 3 se devuelven todos los directorios de conferencia que se hospedan en el servicio UserServer:atl-cs-001.litwareinc.com. Para esto, el comando primero llama al cmdlet **Get-CsConferenceDirectory** sin ningún parámetro para devolver una recopilación de todos los directorios de conferencia que se encuentran en su organización. A continuación, esta recopilación se canaliza al cmdlet **Where-Object**, que selecciona únicamente esos directorios en que el ServiceID coincide con el valor "UserServer:atl-cs-001.litwareinc.com".

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"}

## Descripción detallada

Al crear un Identificador Uniforme de Recursos (URI) de conferencia de acceso telefónico local, se le asigna direcciones SIP únicas. Sin embargo, las direcciones SIP resultan difíciles de convertir para los dispositivos no compatibles con SIP; por ejemplo, un teléfono de la red telefónica conmutada (RTC) no puede convertir una dirección SIP. Debido a esto, Lync Server usa directorios de conferencia para ayudar a estos dispositivos a localizar y conectarse a las conferencias de acceso telefónico local. Esto se realiza creando un directorio de conferencia SIP que se asocia con cada URI de conferencia de acceso telefónico y se identifica con un valor entero en lugar de un URI de SIP. Los teléfonos de RTC y otros dispositivos pueden usar estos números (en lugar de un URI de SIP) cuando se conectan a conferencias; el número de directorio se incluye en la identificación de conferencia de RTC que escriben los usuarios cuando se conectan a una conferencia de acceso telefónico local.

El cmdlet **Get-CsConferenceDirectory** lo habilita para devolver información sobre todos los directorios de conferencia configurados en su organización.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Get-CsConferenceDirectory** en forma local: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDirectory"}

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
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Le permite usar comodines para especificar la identidad del directorio de conferencia (o directorios) que deben recuperarse. Debido a que las identidades de directorio son numéricas, este parámetro puede ser de valor mínimo. Sin embargo, esta sintaxis devolverá todos los directorios de conferencia que tengan una identidad que comience con el número 3: -Filter &quot;3*&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador numérico (por ejemplo, 7) del directorio de conferencia que debe devolverse. Si este parámetro se omite, el cmdlet <strong>Get-CsConferenceDirectory</strong> devuelve información sobre todos los directorios de conferencia en uso en la organización.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos del directorio de conferencias de la réplica local de Almacén de administración central, en lugar del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsConferenceDirectory** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsConferenceDirectory** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Vea también

#### Otros recursos

[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

