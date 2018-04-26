---
title: Get-CsTenantFederationConfiguration
TOCTitle: Get-CsTenantFederationConfiguration
ms:assetid: e5f836d0-6066-4c23-9594-6e3f1cbd39ef
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994072(v=OCS.15)
ms:contentKeyID: 52061956
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantFederationConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre las opciones de configuración de federación para sus inquilinos de Microsoft Lync Online. Las opciones de configuración de federación se usan para determinar con qué dominios (si existe alguno) se pueden comunicar sus usuarios.

El cmdlet **Get-CsTenantFederationConfiguration** solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Get-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-LocalStore] [-Verbose] Get-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-Filter <String>] [-LocalStore] [-Verbose]

## Ejemplos

## Ejemplo 1

El comando del ejercicio 1 devuelve información sobre la configuración de federación para el inquilino cuyo id. de inquilino es "bf19b7db-6960-41e5-a139-2aa373474354". Los id. de los inquilinos se pueden recuperar usando un comando como este:

Get-CsTenant | Select-Object TenantID

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

El parámetro Tenant es opcional. También puede llamar a Get-CsTenantFederationConfiguration usando esta sintaxis:

    Get-CsTenantFederationConfiguration

## Ejemplo 2

En el ejemplo 2, se devuelve información para todos los dominios encontrados en la lista de dominios permitidos para la federación del inquilino bf19b7db-6960-41e5-a139-2aa373474354. (La lista de permitidos representa todos los dominios con los que el inquilino se puede federar). Para hacer esto, el comando llama primero al cmdlet **Get-CsTenantFederationConfiguration** para devolver información de federación sobre el inquilino especificado. Luego, esta información se canaliza al cmdlet **Select-Object**, que usa ExpandProperty para "expandir" la propiedad AllowedList. Expandir una propiedad significa mostrar en pantalla toda la información almacenada en esa propiedad con un formato de fácil lectura.

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty AllowedList

## Ejemplo 3

El comando anterior devuelve la configuración de federación de todos los inquilinos que están actualmente en uso en la organización. Para hacer esta tarea, el comando llama primero al cmdlet **Get-CsTenant** sin parámetros, lo cual devuelve una colección de todos los inquilinos disponibles. Luego, esta colección se canaliza al cmdlet **ForEach-Object**. ForEach-Object toma cada uno de los inquilinos de la colección y llama al cmdlet **Get-CsTenantFederationConfiguration** usando el valor de propiedad TenantID (devuelto por el cmdlet **Get-CsTenant**) para representar el id. del inquilino.

    Get-CsTenant | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId}

## Ejemplo 4

En el ejemplo 4, solo se devuelve información sobre la configuración de federación para los inquilinos que no permiten la federación con usuarios públicos. Para ello, el comando llama primero al cmdlet **Get-CsTenant** sin ningún parámetro para devolver una recopilación de todos los inquilinos configurados para su uso en la organización. Luego esa colección se canaliza al cmdlet **ForEach-Object**, que toma cada inquilino de la colección y usa el cmdlet **Get-CsTenantFederationConfiguration** para devolver información sobre la configuración de federación. Luego se canaliza el conjunto completo de información de configuración de federación al cmdlet **Where-Object**, que solo escoge los inquilinos en los que la propiedad AllowPublicUsers es igual a (-eq) $False.

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId} | Where-Object {$_.AllowPublicUsers -eq $False}

## Descripción detallada

La federación es un servicio que permite a los usuarios intercambiar información de mensajería instantánea y presencia con usuarios de otros dominios. Con Lync Online, los administradores pueden usar las opciones de configuración de federación para controlar:

  - Si los usuarios pueden comunicarse o no con personas de otros dominios y, si pueden, con qué dominios se pueden comunicar.

  - Si los usuarios pueden comunicarse o no con personas que tienen cuentas en proveedores públicos de mensajería instantánea y de presencia, como Windows Live, AOL y Yahoo.

El cmdlet **Get-CsTenantFederationConfiguration** ofrece a los administradores una forma de devolver información de federación para sus inquilinos de Lync Online. Este cmdlet también se puede usar para revisar las listas de dominios permitidos y bloqueados, listas que se usan para especificar los dominios con los que los usuarios pueden o no comunicarse. Sin embargo, los administradores deben usar el cmdlet **Get-CsTenantPublicProvider** para ver con qué proveedores públicos de mensajería instantánea y presencia se pueden comunicar.

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
<td><p>Le permite usar caracteres comodín para devolver una colección de opciones de configuración de federación de inquilino. Como cada inquilino está limitado a una sola colección global de opciones de configuración de federación, no es necesario usar el parámetro Filter. Sin embargo, esta sintaxis es válida para el cmdlet <strong>Get-CsTenantFederationConfiguration</strong>:</p>
<p>Get-CsTenantFederationConfiguration –Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Especifica la colección de opciones de configuración de federación de inquilino que se va a devolver. Como cada inquilino está limitado a una sola colección global de opciones de configuración de federación, no es necesario incluir este parámetro al llamar al cmdlet <strong>Get-CsTenantFederationConfiguration</strong>. Si decide usar el parámetro Identity, también debe incluir el parámetro Tenant. Por ejemplo:</p>
<p>Get-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración de federación de inquilino a partir de la réplica local del Almacén de administración central en lugar de hacerlo a partir del propio almacén.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuya configuración de federación se está devolviendo. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el id. del inquilino para cada uno de los inquilinos inicie este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si mantiene una sesión remota de Windows PowerShell y solo se ha conectado a Skype Empresarial Online, no tiene que incluir el parámetro Tenant. De hecho, el identificador de inquilino se rellenará automáticamente a partir de la información de conexión en uso. Por lo general, el parámetro Tenant se usa en implementaciones híbridas.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsTenantFederationConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsTenantFederationConfiguration** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Vea también

#### Otros recursos

[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

