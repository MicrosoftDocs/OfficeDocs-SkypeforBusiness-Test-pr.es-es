---
title: Set-CsClientVersionConfiguration
TOCTitle: Set-CsClientVersionConfiguration
ms:assetid: 7cd2e86f-2d31-4db2-9d0f-f1418fd4aba2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398623(v=OCS.15)
ms:contentKeyID: 48275796
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica la colección especificada de opciones de configuración de la versión del cliente. Las opciones de configuración de la versión del cliente determinan si Lync Server comprueba el número de versión de cada aplicación cliente que se conecta al sistema. Si el filtro de la versión del cliente está activado, la capacidad de cada aplicación cliente para obtener acceso al sistema dependerá de las opciones configuradas en la directiva de versión de cliente correspondiente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En el ejemplo 1, se usa el cmdlet **Set-CsClientVersionConfiguration** para modificar la recopilación de configuraciones con la identidad "site:Redmond". En este caso, el parámetro Enabled se configura en False a fin de deshabilitar las opciones de configuración de la versión de cliente.

    Set-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## Ejemplo 2

En el ejemplo anterior, la propiedad DefaultUrl se modifica para todas las opciones de configuración de versión de cliente que se usan actualmente en la organización. Para ello, el comando primero llama al cmdlet **Get-CsClientVersionConfiguration** sin ningún parámetro adicional para devolver todas las opciones de configuración de la versión de cliente. Esa información se canaliza entonces al cmdlet **Set-CsClientVersionConfiguration**, que configura el valor de DefaultUrl en https://litwareinc.com/csclients para cada recopilación de configuración.

    Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration -DefaultURL "https://litwareinc.com/csclients"

## Ejemplo 3

En el ejemplo 3, se modifican todas las opciones de configuración de versión de cliente donde DefaultAction está configurado actualmente en Block. Para ello, el comando primero usa el cmdlet **Get-CsClientVersionConfiguration** para devolver todas las opciones de configuración de la versión de cliente en uso. Luego, esta información se canaliza al cmdlet **Where-Object**, que únicamente selecciona los elementos en los que la propiedad DefaultAction es igual a "Block". A su vez, esa recopilación filtrada después se canaliza al cmdlet **Set-CsClientVersionConfiguration**, que hace dos cosas con cada elemento de la recopilación: 1) configura DefaultAction en BlockWithUrl; y, 2) configura DefaultUrl en https://litwareinc.com/csclients.

    Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block"} | Set-CsClientVersionConfiguration -DefaultAction "BlockWithUrl" -DefaultURL "https://litwareinc.com/csclients"

## Descripción detallada

Lync Server le brinda a los administradores flexibilidad considerable cuando se trata de especificar el software del cliente (también es igual de importante el número de versión del software) que los usuarios pueden usar para iniciar sesión en el sistema. Por ejemplo, no hay ningún motivo técnico que obligue a los usuarios a conectarse a Lync Server con Lync; desde un punto de vista técnico, no hay ninguna razón que impida que los usuarios se conecten con Microsoft Office Communicator 2007 R2.

Sin embargo, puede haber otros motivos, no técnicos, por los que prefiera que los usuarios no se conecten con Office Communicator 2007 R2. Por ejemplo, Office Communicator 2007 R2 no admite todas las funciones y herramientas de Lync y, como consecuencia, los usuarios que inicien sesión con Office Communicator 2007 R2 tendrán una experiencia diferente que los que se conecten con Lync. Eso podría ocasionar dificultades a sus usuarios; además, podría ocasionar dificultades para el personal del departamento de soporte técnico, que deberá brindar soporte para diversas aplicaciones de clientes diferentes.

Si supone un problema para su organización, puede poner en práctica el filtrado de versión de cliente para especificar qué aplicaciones cliente pueden usarse para iniciar sesión en Lync Server. Al instalar Lync Server, se instala y habilita un conjunto de opciones de configuración de versión de cliente. Estas configuraciones se usan para determinar si está habilitado (o no) el filtrado de versión de clientes. Además de la configuración global, también se pueden aplicar opciones de configuración de versión de cliente en el ámbito de sitio; en estos casos, la configuración del sitio tendrá prioridad sobre la configuración global.

El cmdlet **Set-CsClientVersionConfiguration** le permite modificar una recopilación existente de opciones de configuración de versiones de clientes.

Tenga en cuenta que la configuración de versión de cliente no es una característica de seguridad. La tecnología se basa en la información que suministran las aplicaciones cliente y no intenta verificar si una aplicación es realmente la aplicación especificada, ni si el número de versión suministrado es el real.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **Set-CsClientVersionConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionConfiguration"}

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
<td><p><em>DefaultAction</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Indica la acción que se llevará a cabo si un usuario intenta iniciar sesión desde una aplicación cliente con un número de versión que no se encuentre en la directiva de versión de cliente correspondiente. Se debe configurar DefaultAction con uno de los siguientes valores:</p>
<p>Allow: se permitirá el inicio de sesión de la aplicación cliente.</p>
<p>AllowWithUrl: la aplicación cliente podrá iniciar sesión. Además, aparecerá un cuadro de mensaje que mostrará al usuario la dirección URL de una página web en la que el usuario puede descargar la aplicación cliente aprobada. La dirección URL de esta página web debe especificarse como el valor de la propiedad DefaultUrl.</p>
<p>Block: se impedirá que la aplicación cliente inicie sesión.</p>
<p>BlockWithUrl: se impedirá que la aplicación cliente inicie sesión. Sin embargo, el mensaje de acceso denegado mostrará al usuario la dirección URL de una página web en la que el usuario puede descargar la aplicación cliente aprobada. La dirección URL de esta página web debe especificarse como el valor de la propiedad DefaultUrl.</p>
<p>Se ignorará la propiedad si la propiedad Enabled se ha configurado en False. Si la propiedad Enabled está definida en False, no se realizará ningún tipo de filtrado de versión de cliente.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultURL</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Especifica la dirección URL de la página web en la que los usuarios pueden descargar una aplicación cliente aprobada. Si se ha especificado y si DefaultAction se ha configurado en BlockWithURL, esta URL aparecerá en el cuadro de mensaje &quot;Acceso denegado&quot; que se muestra cada vez que un usuario intenta iniciar sesión desde una aplicación de clientes no compatible.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>indica si el filtrado de versión de clientes está habilitado o deshabilitado. Si la propiedad Enabled es True, el servidor comprobará el número de versión de cada aplicación de cliente que intente iniciar sesión; a continuación, el servidor permitirá o denegará el acceso según la directiva de versión de clientes apropiada. Si la propiedad Enabled está definida en False, se permitirá iniciar sesión a cualquier aplicación cliente compatible.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error no graves que se pueden producir al iniciar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Representa el identificador único de las opciones de configuración de versión del cliente que se modificarán. Para modificar las configuraciones globales, use una sintaxis como la siguiente: -Identity global. Para modificar las configuraciones asignadas al ámbito del sitio, use una sintaxis similar a la siguiente: &quot;site:Redmond&quot;.</p>
<p>Si este parámetro no está incluido, el cmdlet <strong>Set-CsClientVersionConfiguration</strong> configurará automáticamente la configuración global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>Objetos ClientVersionPolicy</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration. El cmdlet **Set-CsClientVersionConfiguration** acepta las instancias canalizadas del objeto de la configuración de versión de cliente.

## Tipos de valores devueltos

El cmdlet **Set-CsClientVersionConfiguration** no devuelve ningún valor ni objeto. En su lugar, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vea también

#### Otros recursos

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)

