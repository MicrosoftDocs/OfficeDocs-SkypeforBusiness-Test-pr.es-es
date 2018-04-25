---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412906(v=OCS.15)
ms:contentKeyID: 48276487
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPublicProvider

 

_**Última modificación del tema:** 2015-03-09_

Elimina un proveedor público configurado para usarse en la organización. Un proveedor público es una organización que proporciona mensajería instantánea (MI), presencia y servicios relacionados al público en general. Lync Server incluye tres proveedores públicos configurados, pero no habilitados: Yahoo\!, AIM (AOL) y Messenger (MSN). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando anterior elimina el proveedor público con la identidad Messenger. Una vez completado este comando, Messenger ya no aparecerá en la lista de proveedores públicos configurados y la única forma de volver a establecer la federación con Messenger es volver a crear el proveedor.

    Remove-CsPublicProvider -Identity "Messenger"

## Ejemplo 2

En el ejemplo 2 se eliminan todos los proveedores públicos configurados para su uso en la organización. Para ello, el comando primero usa el cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos configurados actualmente para el uso. A continuación, dicha colección se canaliza al cmdlet **Remove-CsPublicProvider** que, a su vez, elimina todos los proveedores de la colección.

    Get-CsPublicProvider | Remove-CsPublicProvider

## Ejemplo 3

En el ejemplo 3, todos los proveedores públicos que actualmente están deshabilitados se quitan del conjunto de proveedores públicos configurados. Para llevar a cabo esta tarea, el comando primero usa el cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos que actualmente están configurados para su uso. Dicha colección se canaliza al cmdlet **Where-Object**, que únicamente selecciona los proveedores cuya propiedad Enabled sea igual a False. Después, la colección filtrada se canaliza al cmdlet **Remove-CsPublicProvider**, que elimina todos los elementos de la colección.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

## Descripción detallada

La federación es un mecanismo que dos organizaciones pueden usar para establecer una relación de confianza que facilite la comunicación entre los dos grupos. Cuando se ha establecido una federación, los usuarios de ambas organizaciones pueden enviarse mensajes instantáneos, suscribirse para recibir notificaciones de presencia y comunicarse entre sí con aplicaciones SIP, como Lync 2013. Lync Server permite sacar partido de tres tipos de federación: 1) federación directa entre su organización y otra organización; 2) federación entre su organización y un proveedor público y 3) federación entre su organización y un proveedor de hospedaje de terceros.

Un proveedor público es una organización que suministra servicios de comunicación SIP para el público en general. Al establecer una relación de federación con un proveedor público, de hecho establece federación con cualquier usuario que tenga una cuenta hospedada en dicho proveedor. Por ejemplo, si se federa con Messenger (MSN), sus usuarios podrán intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta de mensajería instantánea de Messenger.

Para establecer una federación con un proveedor público es necesario crear y habilitar un proveedor público nuevo. (Además, el proveedor público tendrá que crear una relación de federación con usted). Si, más adelante, decide finalizar la relación, puede usar el cmdlet **Remove-CsPublicProvider** para eliminar el proveedor público. Cuando elimina un proveedor público, el proveedor se quita de la lista de socios federados y la única forma de volver a establecer la relación es volver a crear el proveedor. Si desea suspender una relación de forma temporánea, use el cmdlet **Disable-CsPublicProvider**. Cuando se deshabilita un proveedor público, el proveedor no se elimina de la lista de socios federados; en su lugar, simplemente se marca el proveedor como deshabilitado y se suspende la comunicación entre la organización y el proveedor. Para volver a establecer la relación puede usar simplemente el cmdlet **Enable-CsPublicProvider** para volver a habilitar el proveedor.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Remove-CsPublicProvider** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p>Identificador único para el proveedor público que se va a quitar. La identidad es, por lo general, el nombre del sitio web que proporciona los servicios (por ejemplo, Yahoo!, AOL, MSN, etc.).</p></td>
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
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se produzcan al ejecutar el comando.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. El cmdlet **Remove-CsPublicProvider** acepta entradas canalizadas del objeto de proveedor público.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet elimina las instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vea también

#### Otros recursos

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

