---
title: Remove-CsPrivacyConfiguration
TOCTitle: Remove-CsPrivacyConfiguration
ms:assetid: 32052c51-953d-4278-9425-306245d297ed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425821(v=OCS.15)
ms:contentKeyID: 48274852
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPrivacyConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Quita una colección existente de opciones de configuración de privacidad. Las opciones de configuración de privacidad ayudan a determinar cuánta información ponen los usuarios a disposición de otros usuarios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsPrivacyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se devuelven las opciones de configuración de privacidad asignadas al sitio Redmond. Cuando se eliminan estas opciones, los usuarios del sitio Redmond heredarán automáticamente las opciones de configuración de privacidad globales.

    Remove-CsPrivacyConfiguration -Identity site:Redmond

## EJEMPLO 2

En el ejemplo 2 se eliminan todos los valores de configuración de privacidad asignados en el ámbito de sitio. En primer lugar, el comando llama al cmdlet **Get-CsPrivacyConfiguration** junto con el parámetro de filtro. El valor de filtro "site:\*" garantiza que solo se devolverán aquellos valores cuya propiedad Identity comience por los caracteres "site". A continuación, la colección filtrada se canaliza al cmdlet **Remove-CsPrivacyConfiguration**, que quita los distintos elementos de la colección.

    Get-CsPrivacyConfiguration -Filter "site:*" | Remove-CsPrivacyConfiguration

## EJEMPLO 3

El comando que se muestra en el ejemplo 3 elimina todas las opciones de configuración de privacidad si se inhabilita el modo de privacidad. En primer lugar, el comando llama al cmdlet **Get-CsPrivacyConfiguration** sin ningún parámetro y este devuelve una colección de todos los valores de configuración de privacidad que se usan en la organización. A continuación, esta colección se canaliza al cmdlet **Where-Object**, que solo selecciona aquellos valores cuya propiedad EnablePrivacyMode es igual a False. A continuación, la colección filtrada se canaliza al cmdlet **Remove-CsPrivacyConfiguration**, que elimina los distintos elementos de la colección.

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Remove-CsPrivacyConfiguration

## Descripción detallada

Lync Server permite a los usuarios compartir una gran cantidad de información de presencia con otras personas: pueden publicar una fotografía de sí mismos, ofrecer información de ubicación detallada o poner a disposición de todo el personal de la organización su información de presencia de manera automática (en lugar de que solo sus contactos puedan verla).

Algunos usuarios agradecerán la posibilidad de poner esta información a disposición de sus compañeros y otros pueden ser más reacios a compartir estos datos (por ejemplo, es posible que haya personas que no sepan si incluir o no una foto en los datos de presencia). Como norma general, los usuarios pueden controlar la información que quieren compartir y la que no. Por ejemplo, pueden activar o desactivar una casilla para establecer si la información de ubicación debe compartirse con otros usuarios. Además, los cmdlets de configuración de privacidad permiten a los administradores administrar la configuración de privacidad de los usuarios y, en algunos casos, los administradores pueden habilitar o deshabilitar estos valores. Por ejemplo, si la propiedad AutoInitiateContacts se establece en True, los miembros del equipo se agregarán automáticamente a la lista de contactos de cada usuario (no así si se establece en False).

En otras ocasiones, los administradores pueden configurar los valores predeterminados en Lync Server y permitir que los usuarios puedan cambiar dichos valores. Por ejemplo, los datos de ubicación de los usuarios se publican de manera predeterminada, aunque los usuarios tienen derecho a detener la publicación de ubicación. Si se establece la propiedad PublishLocationDataByDefault en False, los administradores pueden cambiar este comportamiento: en ese caso, los datos de ubicación no se publicarán de manera predeterminada, aunque los usuarios seguirán teniendo derecho a publicarlos si así lo eligen.

Los valores de configuración de privacidad pueden aplicarse en el ámbito global, de sitio y de servicio (aunque solo para el servicio Servidor de usuario). El cmdlet **Remove-CsPrivacyConfiguration** permite eliminar los valores que se han configurado en el ámbito de sitio o de servicio. Por ejemplo, si ejecuta el cmdlet con los valores configurados en el ámbito de sitio, estos se eliminarán y las configuraciones de privacidad de los usuarios se regirán por la colección global. **Remove-CsPrivacyConfiguration** también puede ejecutarse con la colección global, si bien esta no se eliminará. En su lugar, todas las propiedades de esa colección se restablecerán a sus valores predeterminados. Por ejemplo, supongamos que ha cambiado anteriormente la propiedad EnablePrivacyMode a True. Si ahora "elimina" la colección global, EnablePrivacyMode volverá a su valor predeterminado de False.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsPrivacyConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPrivacyConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único de las opciones de configuración de privacidad que se van a quitar. Para quitar la configuración definida en el ámbito de sitio, use la sintaxis del siguiente ejemplo: -Identity site:Redmond. Para quitar configuraciones en el nivel de servicio, utilice sintaxis como la siguiente: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>El cmdlet <strong>Remove-CsPrivacyConfiguration</strong> también puede ejecutarse con la colección global de valores. No obstante, en ese caso la configuración global no se eliminará. En su lugar, todas las propiedades de la colección se restablecerán a sus valores predeterminados.</p></td>
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
<td><p>Suprime la visualización de los mensajes de error que no son graves y que pueden surgir al ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino de Skype Empresarial Online para la que se van a eliminar los valores de configuración de privacidad. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el Id. de inquilino de cada uno de los inquilinos, ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration. El cmdlet **Remove-CsPrivacyConfiguration** acepta la canalización del objeto de configuración de privacidad.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet **Remove-CsPrivacyConfiguration** elimina las instancias existentes del objeto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Vea también

#### Otros recursos

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

