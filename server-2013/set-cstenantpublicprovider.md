---
title: Set-CsTenantPublicProvider
TOCTitle: Set-CsTenantPublicProvider
ms:assetid: 8341d801-bfa1-4c5b-9b80-5d503deebaf7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994047(v=OCS.15)
ms:contentKeyID: 52061701
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantPublicProvider

 

_**Última modificación del tema:** 2015-03-09_

Habilita y deshabilita la comunicación con los proveedores de mensajería instantánea y de presencia de terceros Windows Live, AOL y Yahoo. Cuando se habilita, los usuarios de Microsoft Lync Online pueden intercambiar información de mensajería instantánea y de presencia con usuarios que tienen cuentas en el proveedor público especificado.

El cmdlet **Set-CsTenantPublicProvider** solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Set-CsTenantPublicProvider -Tenant <String> [-Provider <String[]>] [-Verbose] [-WhatIf] [-Confirm]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 habilita la federación con Windows Live para el inquilino cuyo id. de inquilino es bf19b7db-6960-41e5-a139-2aa373474354. Como Windows Live es el único proveedor especificado, los proveedores AOL y Yahoo se deshabilitan al ejecutar el comando.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

## Ejemplo 2

En el ejemplo 2, se habilitan dos proveedores públicos: Windows Live y AOL. Esto significa que solo estará deshabilitado el proveedor público Yahoo en el inquilino especificado.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive","AOL"

## Ejemplo 3

En el ejemplo 3, se ve cómo deshabilitar todos los proveedores públicos en un inquilino determinado. Esto se hace estableciendo la propiedad Provider en una cadena vacía ("").

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

## Ejemplo 4

El comando del ejemplo 4 deshabilita todos los proveedores públicos en todos los inquilinos de Lync Online. Para hacer esto, el comando usa primero el cmdlet **Get-CsTenant** para devolver una colección de todos sus inquilinos. Luego, esta colección se canaliza al cmdlet **ForEach-Object**, que toma cada uno de los inquilinos de la colección, llama al cmdlet **Set-CsTenantPublicProvider** en cada uno de esos inquilinos y deshabilita todos los proveedores públicos. La última tarea se realiza estableciendo la propiedad Provider en una cadena vacía ("").

    Get-CsTenant | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider ""}

## Descripción detallada

Los proveedores públicos son organizaciones que suministran servicios de comunicación SIP para el público en general. Al establecer una relación de federación con un proveedor público, establece la federación con todos los usuarios que tengan una cuenta hospedada en dicho proveedor. Por ejemplo, si se federa con Windows Live, sus usuarios podrán intercambiar mensajes instantáneos e información de presencia con cualquier persona que tenga una cuenta de mensajería instantánea de Windows Live.

Lync Online ofrece a los administradores la opción de configurar la federación con uno o varios de los siguientes proveedores públicos de mensajería instantánea y presencia:

  -   
    Windows Live

  -   
    AOL

  -   
    Yahoo\!

El cmdlet **Set-CsTenantPublicProvider** se puede usar para habilitar o deshabilitar la federación con cualquiera de estos proveedores públicos. Al usar este cmdlet, recuerde que cada vez que ejecute el cmdlet **Set-CsTenantPublicProvider** tiene que especificar todos los proveedores que se deben habilitar. Por ejemplo, supongamos que los tres proveedores están deshabilitados y ejecuta este comando:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

Como cabría esperar, con ese comando se habilita Windows Live, mientras que AOL y Yahoo permanecen deshabilitados.

Supongamos que luego ejecuta este comando:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL"

Este comando habilita AOL, pero también deshabilita Windows Live: esto se debe a que Windows Live no se especificó como parte del valor de parámetro suministrado al parámetro Provider. Si quiere habilitar AOL y mantener Windows Live también habilitado, tiene que especificar AOL y Windows Live al llamar a Set-CsTenantPublicProvider:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Para deshabilitar la federación para los tres proveedores, establezca la propiedad Provider en una cadena vacía (""):

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

Recuerde que habilitar el estado de un proveedor público no significa que los usuarios puedan intercambiar mensajes instantáneos e información de presencia con usuarios que tengan cuentas en ese proveedor. Además de habilitar la federación con el propio proveedor, los administradores también deben establecer la propiedad AllowPublicUsers de las opciones de configuración de federación en True. Si esta propiedad está definida en False, no se permitirá la comunicación con ningún proveedor público sean cuales sean las opciones de configuración de proveedor público.

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
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuya configuración de proveedor público se va a modificar. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para obtener el identificador de inquilino para cada uno de los inquilinos, ejecute este comando:</p>
<pre><code>Get-CsTenant | Select-Object DisplayName, TenantID</code></pre>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String[]</p></td>
<td><p>Indica el proveedor público (o los proveedores) con el que los usuarios podrán comunicarse. Los valores válidos son:</p>
<p>* AOL</p>
<p>* WindowsLive</p>
<p>* Yahoo</p>
<p>Recuerde que, al configurar proveedores públicos, cualquier proveedor incluido en el valor de parámetro Provider se habilitará para su uso, mientras que los que no se incluyan en el valor de parámetro se deshabilitarán. Por ejemplo, esta sintaxis habilita Yahoo y deshabilita Windows Live y AOL:</p>
<p>-Provider &quot;AOL&quot;</p>
<p>Puede habilitar varios proveedores separando los nombres de cada uno con comas:</p>
<p>-Provider &quot;AOL&quot;,&quot;WindowsLive&quot;</p></td>
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

El **Set-CsTenantPublicProvider** acepta instancias canalizadas del objeto Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Tipos de valores devueltos

Ninguno. El cmdlet **Set-CsTenantPublicProvider** modifica las instancias existentes del objeto Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Vea también

#### Otros recursos

[Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

