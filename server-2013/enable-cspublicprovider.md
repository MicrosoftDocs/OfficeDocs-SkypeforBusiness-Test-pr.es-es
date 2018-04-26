---
title: Enable-CsPublicProvider
TOCTitle: Enable-CsPublicProvider
ms:assetid: 98370dfd-9a53-41a8-a1f3-bb7a516c3c5e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398780(v=OCS.15)
ms:contentKeyID: 48276100
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsPublicProvider

 

_**Última modificación del tema:** 2015-03-09_

Habilita un proveedor público configurado para usarse en la organización. Un proveedor público es una organización que proporciona mensajería instantánea, presencia y servicios relacionados al público en general. Lync Server incluye tres proveedores públicos configurados, pero no habilitados: Yahoo\!, AIM (AOL) y Messenger (MSN). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Enable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 habilita el proveedor público con la identidad Messenger. Este comando devuelve un error si Messenger ya está habilitado.

    Enable-CsPublicProvider -Identity "Messenger"

## Ejemplo 2

El comando anterior habilita todos los proveedores públicos que se encuentran deshabilitados. Para iniciar esta tarea, el comando usa primero el cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos configurados para su uso en la organización. Dicha colección se canaliza al cmdlet **Where-Object**, que únicamente selecciona los proveedores cuya propiedad Enabled sea igual a False. Después, la colección filtrada se canaliza al cmdlet **Enable-CsPublicProvider**, que habilita todos los proveedores de la colección.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsPublicProvider

## Ejemplo 3

En el ejemplo 3 se habilitan todos los proveedores públicos que no están ya habilitados, cuyo nivel de comprobación esté configurado como AlwaysVerifiable. Para ello, el comando llama primero al cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos que usa actualmente la organización. Esta colección se canaliza al cmdlet **Where-Object**, que elige los proveedores que cumplen dos criterios: 1) la propiedad VerificationLevel es igual a AlwaysVerifiable, y 2) la propiedad Enabled es igual a False. (El operador -and indica al cmdlet **Where-Object** que los objetos deben cumplir con todos los criterios especificados para poder seleccionarlos). Después, la colección filtrada se canaliza al cmdlet **Enable-CsPublicProvider**, que habilita todos los proveedores de la colección.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysVerifiable" -and $_.Enabled -eq $False} | Enable-CsPublicProvider

## Descripción detallada

La federación es un medio por el cual dos organizaciones pueden establecer una relación de confianza para facilitar la comunicación entre ambas. Cuando se ha establecido una federación, los usuarios de ambas organizaciones pueden enviarse mensajes instantáneos, suscribirse para recibir notificaciones de presencia y comunicarse entre sí con aplicaciones SIP, como Lync 2013. Lync Server permite sacar partido de tres tipos de federación: 1) federación directa entre una organización y otra; 2) federación entre una organización y un proveedor público, y 3) federación entre una organización y un proveedor de hospedaje de terceros.

Un proveedor público es una organización que suministra servicios de comunicación SIP para el público en general. Al establecer una relación de federación con un proveedor público, de hecho establece federación con cualquier usuario que tenga una cuenta hospedada en dicho proveedor. Por ejemplo, si se federa con Messenger (MSN), sus usuarios podrán intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta de mensajería instantánea de MSN Messenger.

Para federarse con un proveedor público, deberá crear y habilitar un nuevo proveedor público. (Además, el proveedor público deberá crear una relación de federación con usted). Los proveedores públicos se pueden habilitar en el momento de su creación o más tarde, con el cmdlet **Enable-CsPublicProvider**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Enable-CsPublicProvider** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsPublicProvider"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
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
<td><p>Identificador único del proveedor público que se habilitará. La identidad es, por lo general, el nombre del sitio web que proporciona los servicios (por ejemplo, Yahoo!, AOL y MSN).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>Objeto DisplayPublicProvider</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. El cmdlet **Enable-CsPublicProvider** acepta entradas canalizadas del objeto de proveedor público.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet habilita instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vea también

#### Otros recursos

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

