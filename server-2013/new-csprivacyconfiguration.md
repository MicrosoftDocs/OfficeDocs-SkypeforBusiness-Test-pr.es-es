---
title: New-CsPrivacyConfiguration
TOCTitle: New-CsPrivacyConfiguration
ms:assetid: 9b7f02d7-93a5-4fa5-a74c-3fe4baf8bbfc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398807(v=OCS.15)
ms:contentKeyID: 48276214
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPrivacyConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea una colección nueva de opciones de configuración de privacidad. La configuración de privacidad ayuda a determinar cuánta información los usuarios ponen a disposición de otros usuarios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsPrivacyConfiguration -Identity <XdsIdentity> [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En el comando del ejemplo 1 se crea una nueva colección de opciones de configuración de privacidad que se aplicarán al sitio Redmond (-Identity site:Redmond). Las nuevas configuraciones habilitan el modo de privacidad; para ello, se agrega el parámetro EnablePrivacyMode y el valor de parámetro se establece en True. Recuerde que se producirá un error en este comando si el sitio Redmond ya tiene una colección de opciones de privacidad.

    New-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $True

## Ejemplo 2

En el ejemplo 2 se demuestra de qué manera se puede usar el parámetro InMemory para crear una colección nueva de opciones de configuración de privacidad que inicialmente existían solo en la memoria. Para ello, se llama al cmdlet **New-CsPrivacyConfiguration** con los parámetros Identity e InMemory; el objeto resultante se almacena en una variable denominada $x. En este momento, la configuración de privacidad solo existe en la memoria; si ejecuta el cmdlet **Get-CsPrivacyConfiguration**, no verá una lista para site:Redmond.

En el segundo comando, el valor de la propiedad EnablePrivacyMode se configura en True. Finalmente, el tercer comando usa el cmdlet **Set-CsPrivacyConfiguration** para transformar esta colección virtual de configuraciones de privacidad en una colección real de configuraciones aplicadas al sitio Redmond. Es absolutamente imprescindible llamar al cmdlet **Set-CsPrivacyConfiguration**: si no llama correctamente a este cmdlet, sus nuevas configuraciones de privacidad nunca se aplicarán al sitio Redmond y desaparecerán por completo cuando finalice su sesión en Windows PowerShell o elimine la variable $x.

    $x = New-CsPrivacyConfiguration -Identity site:Redmond -InMemory
    $x.EnablePrivacyMode = $True
    Set-CsPrivacyConfiguration -Instance $x

## Descripción detallada

Lync Server permite a los usuarios compartir mucha información de presencia con otras personas: pueden publicar una fotografía de sí mismos; ofrecer información de ubicación detallada; poner a disposición de todo el personal de la organización su información de presencia de manera automática (en lugar de que solo sus contactos puedan verla).

Algunos usuarios aprovecharán estas funciones para que sus compañeros de trabajo puedan tener acceso a esta información, aunque otros pueden preferir no compartir estos datos. (Por ejemplo, algunas personas pueden preferir no incluir su foto en los datos de presencia). Como norma general, los usuarios pueden controlar qué información quieren compartir y cuál no. Por ejemplo, pueden activar o desactivar una casilla para determinar si su información de ubicación se comparte con los demás. Además, los cmdlets de configuración de privacidad permiten a los administradores controlar las opciones de privacidad de los usuarios. En algunos casos, los administradores pueden habilitar o deshabilitar configuraciones; por ejemplo, si la propiedad AutoInitiateContacts está definida en True, los miembros del equipo se agregarán automáticamente a la lista de contactos de cada usuario; si está definida en False, los miembros del equipo no se agregarán automáticamente a la lista de contactos de cada usuario.

En otros casos, los administradores pueden configurar los valores predeterminados en Lync y permitir que los usuarios puedan cambiar dichos valores. Por ejemplo, de manera predeterminada, se publican datos para los usuarios, aunque estos tienen el derecho a detener la publicación de la ubicación. Al configurar la propiedad PublishLocationDataByDefault en False, los administradores pueden cambiar este comportamiento: en ese caso, los datos de la ubicación no se publicarán de manera predeterminada, aunque los usuarios aún tendrán derecho a publicar estos datos si así lo desean.

La configuración de privacidad se puede aplicar en el ámbito global, en el ámbito del sitio y en el ámbito de servicio (aunque únicamente para el servicio de servidor usuario). El cmdlet **New-CsPrivacyConfiguration** le permite crear nuevas opciones de configuración de privacidad para aplicar a un sitio o servicio. (No se pueden crear colecciones nuevas en el ámbito global). Recuerde que cada servicio o sitio individual puede tener, como máximo, una única colección de opciones de configuración de privacidad: si intenta crear una colección nueva para el sitio Redmond y ese sitio ya tiene una colección de configuraciones de privacidad, se producirá un error en el comando.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **New-CsPrivacyConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPrivacyConfiguration"}

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
<td><p>Identificador único de las opciones de configuración de privacidad que se crearán. Para crear una colección de configuraciones en el ámbito del sitio, use una sintaxis similar a la siguiente: -Identity site:Redmond. Para crear una configuración en el ámbito del servicio, use una sintaxis similar a la siguiente: -Identity service:UserServer:atl-cs-001.litwareinc.com. Las configuraciones de privacidad solo se pueden crear para el servicio de servidor de usuarios. Se producirá un error si intenta aplicar estas configuraciones a cualquier otro servicio.</p>
<p>Recuerde que se producirá un error en el comando si ya existen opciones de configuración de privacidad para el servicio o sitio especificado. De la misma forma, se producirá un error en el comando si intenta crear una nueva colección de configuraciones globales.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en True, Lync agregará automáticamente el director y los informes directos a su lista de contactos. El valor predeterminado es True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en True, la foto del usuario se publicará en Lync de manera automática. Si se encuentra en False, la foto del usuario no estará disponible salvo que, explícitamente, seleccione la opción Dejar que otros vean mi foto. El valor predeterminado es True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si está definido en True, los usuarios podrán habilitar el modo de privacidad avanzada. En el modo de privacidad avanzada, solo las personas de la lista de contactos podrán ver su información de presencia. Si se establece en False, su información de presencia estará disponibles para todas las personas de la organización. El valor predeterminado es False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error no graves que se pueden producir al iniciar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en True, los datos de ubicación se publicarán en Lync de manera automática. Si se establece en False, los datos de ubicación no estarán disponibles salvo que el usuario seleccione explícitamente la opción Mostrar mi ubicación a los contactos. El valor predeterminado es True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino de Skype Empresarial Online para la que se están creando las nuevas opciones de configuración de privacidad. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el Id. de inquilino de cada uno de los inquilinos, ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Ninguno. El cmdlet **New-CsPrivacyConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **New-CsPrivacyConfiguration** crea nuevas instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Vea también

#### Otros recursos

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

