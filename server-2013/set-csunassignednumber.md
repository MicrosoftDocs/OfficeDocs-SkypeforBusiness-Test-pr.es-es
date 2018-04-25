---
title: Set-CsUnassignedNumber
TOCTitle: Set-CsUnassignedNumber
ms:assetid: e7f52423-58d1-410a-9071-731bde45d3d4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399033(v=OCS.15)
ms:contentKeyID: 48277015
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUnassignedNumber

 

_**Última modificación del tema:** 2015-03-09_

Modifica un intervalo de números no asignados y las reglas de enrutamiento que se aplican a dichos números. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se modifica el intervalo de números no asignados llamado UNSet1. Primero transferimos al parámetro Identity el valor UNSet1, el nombre del intervalo de números sin asignar que queremos modificar. Usamos los parámetros NumberRangeStart (+14255551000) y NumberRangeEnd (+14255551900) para definir el intervalo de números sin asignar al que se aplicará el anuncio o el operador automático especificado.

    Set-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## Ejemplo 2

En este ejemplo, se modifica el anuncio de todas las configuraciones de intervalo de números no asignados que tengan un anuncio con la cadena "Welcome" en el nombre. Primero, se llama al cmdlet **Get-CsUnassignedNumber** para recuperar todas las configuraciones de números no asignados. La recopilación de configuraciones se canaliza al cmdlet **Where-Object**, que selecciona solo las configuraciones en las que la propiedad AnnouncementName contiene (-match) la cadena de caracteres Welcome. Estas configuraciones se canalizan al cmdlet **Set-CsUnassignedNumber**, donde modificamos el identificador de servidor de aplicación del servicio de anuncios (ApplicationServer:redmond.litwareinc.com) con el parámetro AnnouncementService, y el nombre del nuevo anuncio (Help Desk Announcement) con el parámetro AnnouncementName. Tenga en cuenta que, si el nuevo anuncio conserva el mismo identificador de servicio aunque tenga otro nombre, deberá especificar el identificador de servicio junto con el nombre.

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Set-CsUnassignedNumber -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Help Desk Announcement"

## Descripción detallada

Los números sin asignar son números de teléfono que se han asignado a una organización pero no a usuarios o teléfonos específicos. Lync Server puede configurarse para enrutar las llamadas recibidas a determinados destinos cuando se llama a un número sin asignar. Este cmdlet modifica la configuración que determina dicho enrutamiento.

Para modificar las opciones de este cmdlet, el sistema debe tener definido Announcements o tener configurado un operador automático de Mensajería unificada de Exchange. Para averiguar si Announcements está definido, llame al cmdlet **Get-CsAnnouncement**. Para crear un Announcement nuevo, llame al cmdlet **New-CsAnnouncement**. Para comprobar la configuración de operador automático de Mensajería unificada de Exchange, ejecute el cmdlet **Get-CsExUmContact**.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **Set-CsUnassignedNumber** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>Requerido</p></td>
<td><p>Cadena</p></td>
<td><p>El nombre del anuncio que se usará para administrar las llamadas recibidas en los números del intervalo.</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>Requerido</p></td>
<td><p>Cadena</p></td>
<td><p>Nombre de dominio completo (FQDN) o ID de servicio del servidor de anuncios.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>Requerido</p></td>
<td><p>Cadena</p></td>
<td><p>Número de teléfono del operador automático de Mensajería unificada de Exchange al que se enrutarán las llamadas a números incluidos en el intervalo. El contacto de operador automático de Mensajería unificada de Exchange debe estar configurado para poder asignar un valor a este parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Nombre único del intervalo de números no asignados que se modificará.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>DisplayAnnouncementVacantNumberRange</p></td>
<td><p>Referencia a un objeto que contiene configuraciones de números no asignados. Este objeto debe ser de tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange y puede recuperarse llamando al cmdlet <strong>Get-CsUnassignedNumber</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Último número del intervalo de números no asignados. Debe ser mayor o igual que el número de NumberRangeStart. Para especificar un único número, use el mismo número para los valores NumberRangeStart y NumberRangeEnd.</p>
<p>El número debe tener el mismo formato que la expresión regular (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Esto significa que el número puede comenzar con la cadena de caracteres tel: (si no especifica la cadena de caracteres, se agregará automáticamente), un signo más (+), y un dígito del 1 al 9. El número de teléfono puede tener hasta 17 dígitos y puede estar seguido de una extensión en formato &quot;;ext=número de extensión&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Primer número del intervalo de números no asignados. Debe ser menor o igual que el valor de NumberRangeEnd.</p>
<p>El número debe tener el mismo formato que la expresión regular (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Esto significa que el número puede comenzar con la cadena de caracteres tel: (si no especifica la cadena de caracteres, se agregará automáticamente), un signo más (+), y un dígito del 1 al 9. El número de teléfono puede tener hasta 17 dígitos y puede estar seguido de una extensión en formato &quot;;ext=número de extensión&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Es posible que los números no asignados se superpongan. Si un número está incluido en varios intervalos, se usará el intervalo con la prioridad más alta.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange. Acepta la entrada por canalización de objetos de números sin asignar.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Modifica un objeto de tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

## Vea también

#### Otros recursos

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

