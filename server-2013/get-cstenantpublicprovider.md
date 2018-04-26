---
title: Get-CsTenantPublicProvider
TOCTitle: Get-CsTenantPublicProvider
ms:assetid: 0d949ec2-206d-4979-a3be-a5578ae93ed3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994016(v=OCS.15)
ms:contentKeyID: 52061592
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantPublicProvider

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información que indica si los usuarios de Microsoft Lync Online pueden comunicarse con personas que tengan cuentas en los proveedores de terceros de mensajería instantánea y presencia Windows Live, AOL y Yahoo.

Este cmdlet solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Get-CsTenantPublicProvider -Tenant <String> [-Verbose]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve información de proveedor público para el inquilino cuyo ID de inquilino es "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

El parámetro Tenant es opcional. También puede llamar a Get-CsTenantPublicProvider usando esta sintaxis:

    Get-CsTenantPublicProvider

## Ejemplo 2

El comando anterior devuelve información detallada sobre el estado de todos los proveedores públicos asignados al inquilino bf19b7db-6960-41e5-a139-2aa373474354. Para hacer esto, el comando usa primero el cmdlet **Get-CsTenantPublicProvider** para devolver información de proveedor público para el inquilino especificado. Luego, esta información se canaliza al cmdlet **Select-Object**, que usa el parámetro ExpandProperty para "expandir" el valor de la propiedad DomainPICStatus. Expandir una propiedad significa mostrar en pantalla todos los valores almacenados en esa propiedad con un formato de fácil lectura.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Un comando como este se usaría en una implementación híbrida de Lync Server 2013.

## Ejemplo 3

El comando que se muestra en el ejemplo 3 es una variación del comando del ejemplo 2, pero en el ejemplo 3 la información de proveedor público devuelta al "expandir" el valor de la propiedad DomainPICStatus se canaliza, a su vez, al cmdlet **Where-Object**. Luego, el cmdlet **Where-Object** elige solo los proveedores cuya propiedad Status está establecida en Enabled. El efecto neto es mostrar solo los proveedores públicos que están habilitados para el uso.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus | Where-Object {$_.Status -eq "Enabled"}

## Descripción detallada

Los proveedores públicos son organizaciones que suministran servicios de comunicación SIP para el público en general. Al establecer una relación de federación con un proveedor público, establece la federación con todos los usuarios que tengan una cuenta hospedada en dicho proveedor. Por ejemplo, si se federa con Windows Live, sus usuarios podrán intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta de mensajería instantánea de Windows Live.

Lync Online ofrece a los administradores la opción de configurar la federación con uno o varios de los siguientes proveedores públicos de mensajería instantánea y presencia:

  - Windows Live

  - AOL

  - Yahoo\!

Los administradores pueden usar el cmdlet **Get-CsTenantPublicProvider** para determinar cuál de esos proveedores se ha habilitado para la federación (en caso de que alguno esté habilitado). Al llamar al cmdlet **Get-CsTenantPublicProvider**, obtendrá una información como esta:

    PublicProviderSet     DomainPicStatus
    ------------------    ------------------------
    True                  {Microsoft.Rtc.Management.Hosted.DomainPICStatus}

La propiedad PublicProviderSet indica si la federación se ha habilitado o no para uno o varios proveedores públicos. Si PublicProviderSet es igual a True, significa que la federación se ha habilitado al menos con un proveedor; si PublicProviderSet es igual a False, significa que la federación está deshabilitada para los tres proveedores públicos (Windows Live, AOL y Yahoo). Para determinar el estado real de cada proveedor, use este comando:

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Recuerde que habilitar el estado de un proveedor público no significa que los usuarios puedan intercambiar mensajes instantáneos e información de presencia con usuarios que tengan cuentas en ese proveedor. Además de habilitar la federación con el propio proveedor, los administradores también deben establecer la propiedad AllowPublicUsers de las opciones de configuración de federación en True. Si esta propiedad está definida en False, no se permitirá la comunicación con ningún proveedor público sean cuales sean las opciones de configuración de proveedor público.

Si desea más información, consulte el tema de ayuda relativo al cmdlet **Set-CsTenantFederationConfiguration**.

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
<td><p><em>Tenant</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuya configuración de proveedor público se va a devolver. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el id. del inquilino para cada uno de los inquilinos inicie este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si mantiene una sesión remota de Windows PowerShell y solo se ha conectado a Skype Empresarial Online, no tiene que incluir el parámetro Tenant. De hecho, el identificador de inquilino se rellenará automáticamente a partir de la información de conexión en uso. Por lo general, el parámetro Tenant se usa en implementaciones híbridas.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsTenantPublicProvider** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsTenantPublicProvider** devuelve instancias del objeto Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Vea también

#### Otros recursos

[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md)

