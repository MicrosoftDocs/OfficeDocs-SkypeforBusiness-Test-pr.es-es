---
title: Get-CsPublicProvider
TOCTitle: Get-CsPublicProvider
ms:assetid: c122505d-7209-4dcb-a888-5c73f58fa68a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412945(v=OCS.15)
ms:contentKeyID: 48276562
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPublicProvider

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los proveedores públicos configurados para el uso en una organización. Un proveedor público es una organización que proporciona servicios de mensajería instantánea, presencia y otros servicios relacionados con el público en general. Lync Server tiene tres proveedores públicos configurados pero no habilitados: Yahoo\!, AIM (AOL) y Messenger (MSN). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPublicProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve una colección de todos los proveedores públicos que están configurados para su uso en la organización. Al llamar al cmdlet **Get-CsPublicProvider** sin parámetros adicionales, siempre se devuelve la colección completa de proveedores públicos.

    Get-CsPublicProvider

## Ejemplo 2

En el ejemplo 2, se devuelven todos los proveedores públicos que tienen la identidad Messenger. Dado que las identidades deben ser únicas entre los proveedores públicos (y entre los proveedores de hospedaje), este comando siempre devolverá, como mucho, un elemento.

    Get-CsPublicProvider -Identity "Messenger"

## Ejemplo 3

El comando anterior devuelve todos los proveedores públicos que tienen una identidad que comienza por la letra W. Para ello, se incluye el parámetro Filter y el valor de filtro "W\*".

    Get-CsPublicProvider -Filter W*

## Ejemplo 4

El comando del ejemplo 4, devuelve una colección de todos los proveedores públicos que están deshabilitados. Para ello, el comando primero llama al cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos configurados para su uso en la organización. Dicha colección se canaliza al cmdlet **Where-Object**, que únicamente selecciona los proveedores cuya propiedad Enabled sea igual a False.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False}

## Ejemplo 5

El ejemplo 5 devuelve todos los proveedores públicos cuya propiedad VerificationLevel esté establecida en AlwaysUnverifiable o UseSourceVerification. (Los niveles de comprobación se pueden definir en AlwaysUnverifiable, UseSourceVerification o AlwaysVerifiable). Para realizar esta tarea, el comando primero llama al cmdlet **Get-CsPublicProvider** para devolver una colección de todos los proveedores públicos configurados para su uso en la organización. La colección se canaliza al cmdlet **Where-Object**, que únicamente selecciona los proveedores cuya propiedad VerificationLevel no sea igual a AlwaysVerifiable. El efecto resultante es que solo se seleccionan los proveedores cuya propiedad VerificationLevel esté establecida en AlwaysUnverifiable o UseSourceVerification.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"}

## Descripción detallada

La federación es un mecanismo que dos organizaciones pueden usar para establecer una relación de confianza que facilite la comunicación entre los dos grupos. Cuando se ha establecido una federación, los usuarios de ambas organizaciones pueden enviarse mensajes instantáneos, suscribirse para recibir notificaciones de presencia y comunicarse entre sí con aplicaciones SIP, como Lync 2013. Lync Server permite sacar partido de tres tipos de federación: 1) federación directa entre su organización y otra organización; 2) federación entre su organización y un proveedor público y 3) federación entre su organización y un proveedor de hospedaje de terceros.

Un proveedor público es una organización que suministra servicios de comunicación SIP para el público en general. Al establecer una relación de federación con un proveedor público, de hecho establece federación con cualquier usuario que tenga una cuenta hospedada en dicho proveedor. Por ejemplo, si se federa con Messenger (MSN), sus usuarios podrán intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta de mensajería instantánea de Messenger.

Para establecer una federación con un proveedor público es necesario crear y habilitar un proveedor público nuevo. (Además, el proveedor público tendrá que crear una relación de federación con usted). El cmdlet **Get-CsPublicProvider** permite devolver información sobre los proveedores públicos que se han configurado para el uso en la organización.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Get-CsPublicProvider** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPublicProvider"}

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
<td><p>Permite usar valores comodín para devolver uno o más proveedores públicos. Por ejemplo, para devolver una colección de todos los proveedores públicos que tengan una identidad que comience por la letra Y, use esta sintaxis: -Filter &quot;Y*&quot;. Para devolver una colección de todos los proveedores públicos que incluyan el valor de cadena de caracteres &quot;Windows&quot; en su identidad, use esta sintaxis: -Filter &quot;*Windows*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador único del proveedor público que se va a devolver. La identidad es, por lo general, el nombre del sitio web que proporciona los servicios (por ejemplo, Yahoo!, AOL, MSN, etc.).</p>
<p>No puede usar caracteres comodín para especificar la identidad. Si desea usar caracteres comodín para devolver uno o más proveedores públicos, use el parámetro Filter.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos del proveedor público de la réplica local de Almacén de administración central en lugar de recuperarlos de Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsPublicProvider** no acepta entradas canalizadas.

## Tipos de valores devueltos

Devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vea también

#### Otros recursos

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

