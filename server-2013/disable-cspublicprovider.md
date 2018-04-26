---
title: Disable-CsPublicProvider
TOCTitle: Disable-CsPublicProvider
ms:assetid: df1338ea-fe6d-45da-a39c-86108bb54ef5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398984(v=OCS.15)
ms:contentKeyID: 48276898
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsPublicProvider

 

_**Última modificación del tema:** 2015-03-09_

Habilita un proveedor público configurado para usarse en la organización. Un proveedor público es una organización que proporciona mensajería instantánea, presencia y servicios relacionados al público en general. Lync Server incluye tres proveedores públicos configurados, pero no habilitados: Yahoo\!, AIM (AOL) y Messenger (MSN). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Disable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando anterior deshabilita el proveedor público con la identidad Messenger. Este comando devuelve un error si MSN ya se deshabilitó.

    Disable-CsPublicProvider -Identity "Messenger"

## Ejemplo 2

En el ejemplo 2 se deshabilitan todos los proveedores públicos que hay habilitados. Para ello, el comando usa primero el cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos en uso en la organización. Dicha colección se canaliza al cmdlet **Where-Object**, que únicamente selecciona los proveedores cuya propiedad Enabled sea igual a True. A su vez, esta colección filtrada se canaliza al cmdlet **Disable-CsPublicProvider**, que deshabilita cada proveedor de la colección.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsPublicProvider

## Ejemplo 3

El comando que se muestra en el ejemplo 3 deshabilita todos los proveedores públicos que hay habilitados y cuyo nivel de verificación sea AlwaysVerifiable. Para realizar esta tarea, el comando primero llama al cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos en uso en la organización. Esta colección se canaliza al cmdlet **Where-Object**, que selecciona los proveedores que cumplen dos criterios: 1) la propiedad VerificationLevel es igual a AlwaysVerifiable, y 2) la propiedad Enabled es igual a True. (El operador -and indica al cmdlet **Where-Object** que los objetos deben cumplir todos los criterios especificados para poderse seleccionar). A continuación, la colección filtrada se canaliza al cmdlet **Disable-CsPublicProvider**, que deshabilita cada proveedor de la colección.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsPublicProvider

## Descripción detallada

La federación es un mecanismo mediante el cual dos organizaciones pueden establecer una relación de confianza que facilita la comunicación entre los dos grupos. Cuando se ha establecido una federación, los usuarios de ambas organizaciones pueden enviarse mensajes instantáneos, suscribirse para recibir notificaciones de presencia y comunicarse entre sí a través de aplicaciones SIP, como Lync 2013. Lync Server permite sacar partido de tres tipos de federación: 1) federación directa entre su organización y otra organización; 2) federación entre su organización y un proveedor público y 3) federación entre su organización y un proveedor de hospedaje de terceros.

Un proveedor público es una organización que proporciona servicios de comunicación SIP (Protocolo de inicio de sesión) para el público en general. Cuando usted establece una relación de federación con un proveedor público, de hecho establece una federación con cualquier usuario que tenga una cuenta hospedada con dicho proveedor. Por ejemplo, si se federa con Messenger (MSN), sus usuarios podrán intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta de mensajería instantánea de Messenger.

Para establecer una federación con un proveedor público es necesario crear y habilitar un proveedor público nuevo. (Además, el proveedor público tendrá que crear una relación de federación con usted.) Cuando crea un proveedor público, tiene la opción de habilitar o deshabilitar dicha relación de federación. Si se habilita un proveedor público, los usuarios de la organización pueden intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta con el proveedor público. Si se deshabilita un proveedor público, se suspenderá la posibilidad de comunicarse con personas que tengan cuentas con el proveedor público, y seguirá suspendida hasta que el proveedor la vuelva a habilitar. Si desea suspender una relación de proveedor de forma temporal, puede usar el cmdlet **Disable-CsPublicProvider**. Si prefiere eliminar el proveedor, use el cmdlet **Remove-CsPublicProvider**.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Disable-CsPublicProvider**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsPublicProvider"}

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
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan ocurrir al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador único para el proveedor público que se va a deshabilitar. La identidad es, por lo general, el nombre del sitio web que proporciona los servicios (por ejemplo, Yahoo!, AOL, MSN, etc.).</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. El cmdlet **Disable-CsPublicProvider** acepta las instancias transferidas del objeto de proveedor público.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet deshabilita instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vea también

#### Otros recursos

[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

