---
title: Set-CsTenantFederationConfiguration
TOCTitle: Set-CsTenantFederationConfiguration
ms:assetid: e13c2f55-7a68-4174-a0da-5eec8c65f64c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994080(v=OCS.15)
ms:contentKeyID: 52061896
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantFederationConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Administra las opciones de configuración de federación para los inquilinos de Microsoft Lync Online. Esta configuración determinará los dominios con los que los usuarios pueden comunicarse (si los hay).

El cmdlet **Set-CsTenantFederationConfiguration** solo puede usarse con Skype Empresarial Online.

## Sintaxis

    Set-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Force] [-Verbose] [-WhatIf] [-Confirm]Set-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Instance <PSObject>] [-Force] [-Verbose] [-WhatIf] [-Confirm]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 deshabilita la comunicación con los proveedores públicos para el inquilino con TenantId "bf19b7db-6960-41e5-a139-2aa373474354".

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowPublicUsers $False

Tenga en cuenta que el parámetro Tenant es opcional. Si no se activa, Windows PowerShell insertará automáticamente el identificador de inquilino correcto en función de la información de conexión del usuario.

## Ejemplo 2

El ejemplo 2 muestra cómo deshabilitar la comunicación con los proveedores públicos para todos los inquilinos de una organización. En primer lugar, el comando llama al cmdlet **Get-CsTenant** para que devuelva una colección de todos los inquilinos disponibles. La colección se canaliza hacia el cmdlet **Select-Object**, que solo selecciona la propiedad TenantId para los distintos elementos de la colección. A continuación, la colección de identificadores de inquilino se canaliza hacia el cmdlet **ForEach-Object**. El cmdlet F**orEach-Object** ejecuta el cmdlet **Set-CsTenantFederationConfiguration** para cada identificador de inquilino y establece la propiedad AllowPublicUsers en Falso ($False).

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantId -AllowPublicUsers $False}

## Ejemplo 3

En el ejemplo 3 se asigna el dominio fabrikam.com como único dominio de la lista de dominios bloqueados del inquilino con TenantId "bf19b7db-6960-41e5-a139-2aa373474354". Para ello, el primer comando del ejemplo usa el cmdlet **New-CsEdgeDomainPattern** para crear un objeto de dominio nuevo para fabrikam.com, que se almacena en una variable llamada $x.

El segundo comando del ejemplo usa el cmdlet **Set-CsTenantFederationConfiguration** para actualizar la lista de dominios bloqueados. Con el método Replace se garantiza que la lista de dominios bloqueados existente se reemplazará por la nueva lista, que únicamente contiene el dominio fabrikam.com.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Replace=$x}

## Ejemplo 4

Los comandos del ejemplo 4 quitan fabrikam.com de la lista de dominios bloqueados que ha definido el inquilino con TenantId "bf19b7db-6960-41e5-a139-2aa373474354". Para ello, el primer comando del ejemplo usa el cmdlet **New-CsEdgeDomainPattern** para crear un objeto de dominio para fabrikam.com. El objeto de dominio obtenido se almacena en una variable llamada $x.

El segundo comando del ejemplo usa el cmdlet **Set-CsTenantFederationConfiguration** y el método Remove para quitar fabrikam.com de la lista de dominios bloqueados del inquilino especificado.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Remove=$x}

## Ejemplo 5

Los comandos del ejemplo 5 agregan el dominio fabrikam.com a la lista de dominios bloqueados que ha definido el inquilino con TenantId "bf19b7db-6960-41e5-a139-2aa373474354". Para ello, el primer comando del ejemplo usa el cmdlet **New-CsEdgeDomainPattern** para crear un objeto de dominio para fabrikam.com, que se almacena en una variable llamada $x.

Tras crear el objeto de dominio, el segundo comando usa el cmdlet **Set-CsTenantFederationConfiguration** y el método Add para agregar fabrikam.com a los dominios que ya se encuentran en la lista de dominios bloqueados.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Add=$x}

## Ejemplo 6

El ejemplo 6 muestra cómo quitar todos los dominios que se han asignado a la lista de dominios bloqueados de un inquilino específico. Para ello, simplemente se debe incluir el parámetro BlockedDomains y establecer su valor en NULL. Cuando se complete el comando, se borrará la lista de dominios bloqueados del inquilino con TenantId "bf19b7db-6960-41e5-a139-2aa373474354".

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $Null

## Descripción detallada

La federación es un servicio que permite a los usuarios intercambiar información de presencia y mensajería instantánea con usuarios de otros dominios. Lync Online permite a los administradores usar las opciones de configuración de federación para controlar:

  -   
    Si los usuarios pueden o no comunicarse con personas de otros dominios y, en caso afirmativo, cuáles son estos dominios.

  -   
    Si los usuarios pueden o no comunicarse con personas que disponen de cuentas con proveedores de presencia y servicios de mensajería instantánea pública, como Windows Live, AOL y Yahoo.

Los administradores pueden usar el cmdlet **Set-CsTenantFederationConfiguration** para habilitar y deshabilitar la federación con otros dominios y proveedores públicos. También puede usarse para indicar de forma expresa los dominios con los que se permite (o no) la comunicación de los usuarios. No obstante, los administradores deben usar el cmdlet **Set-CsTenantPublicProvider** para indicar cuáles son los proveedores de presencia y servicios de mensajería instantánea pública con los que los usuarios no pueden comunicarse.

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
<td><p><em>AllowedDomains</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.IAllowedDomainsChoice</p></td>
<td><p>Objetos de dominio (que se han creado con los cmdlets <strong>New-CsEdgeAllowList</strong> o <strong>New-CsEdgeAllowAllKnownDomains</strong>) que representan los dominios con los que se permite la comunicación de los usuarios. Si se usa el cmdlet <strong>New-CsEdgeAllowAllKnownDomains</strong>, los usuarios podrán comunicarse con cualquier dominio, independientemente de que aparezca o no en la lista de dominios bloqueados. Si en cambio se usa el cmdlet <strong>New-CsEdgeAllowList</strong>, los usuarios solo podrán comunicarse con los dominios que se encuentren en sus listas de dominios permitidos.</p>
<p>Tenga en cuenta que los valores de cadena no pueden transferirse directamente al parámetro AllowedDomains. En su lugar, deberá crear una referencia de objeto con los cmdlets <strong>New-CsEdgeAllowList</strong> o <strong>New-CsEdgeAllowAllKnownDomains</strong>, y usar la variable de esta referencia como valor de parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en Verdadero (valor predeterminado), los usuarios podrán comunicarse con usuarios de otros dominios. No podrán hacerlo si se establece en Falso, independientemente de los valores que se hayan asignado a las propiedades AllowedDomains y BlockedDomains.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPublicUsers</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en Verdadero (valor predeterminado), los usuarios podrán comunicarse con usuarios que dispongan de cuentas en proveedores de presencia y servicios de mensajería instantánea pública, como Windows Live, Yahoo y AOL. Para administrar la colección de proveedores públicos con los que se permite la comunicación de los usuarios, use el cmdlet Set-CsTenantPublicProvider.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockedDomains</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si la propiedad AllowedDomains se establece en AllowAllKnownDomains, los usuarios podrán comunicarse con usuarios de cualquier dominio, siempre que no aparezcan en la lista de dominios bloqueados. Si esta propiedad se establece en cualquier otro valor, se ignorará la lista de dominios bloqueados y los usuarios solo podrán comunicarse con los dominios que se hayan incluido de forma expresa en la lista de dominios permitidos.</p></td>
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
<td><p>Suprime la visualización de los mensajes de error recuperables que puedan surgir al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Especifica la colección de opciones de configuración de federación de inquilino que debe modificarse. Cada inquilino solo tiene una colección global de opciones de configuración de federación, por lo que no es necesario incluir este parámetro al llamar al cmdlet <strong>Set-CsTenantFederationConfiguration</strong>. Si desea usar el parámetro Identity, deberá incluir también el parámetro Tenant. Por ejemplo:</p>
<p>Set-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Permite transferir al cmdlet una referencia a un objeto, en lugar de establecer valores de parámetro individuales.</p></td>
</tr>
<tr class="odd">
<td><p><em>SharedSipAddressSpace</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en Verdadero, los usuarios que se hospedan en Lync Online usarán el mismo dominio SIP que los que se hospedan en la versión local de Lync Server. El valor predeterminado es Falso, lo que significa que se asignarán dominios SIP diferentes a dos conjuntos de usuarios distintos.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuya configuración de federación se ha modificado. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para que se devuelva el identificador de los distintos inquilinos, ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si mantiene una sesión remota de Windows PowerShell y solo se ha conectado a Skype Empresarial Online, no tiene que incluir el parámetro Tenant. De hecho, el identificador de inquilino se rellenará automáticamente a partir de la información de conexión en uso. Por lo general, el parámetro Tenant se usa en implementaciones híbridas.</p></td>
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

El cmdlet **Set-CsTenantFederationConfiguration** acepta instancias canalizadas del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet **Set-CsTenantFederationConfiguration** modifica instancias existentes del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Vea también

#### Otros recursos

[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

