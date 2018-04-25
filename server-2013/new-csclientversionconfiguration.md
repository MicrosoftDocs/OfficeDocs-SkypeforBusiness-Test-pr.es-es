---
title: New-CsClientVersionConfiguration
TOCTitle: New-CsClientVersionConfiguration
ms:assetid: e7aac850-9e29-4d18-8929-74a89e9355cd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399029(v=OCS.15)
ms:contentKeyID: 48277024
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea una recopilación de configuraciones de versión de cliente. Las opciones de configuración de versión de cliente definen si Lync Server comprueba o no el número de versión de cada aplicación cliente que inicia sesión en el sistema. Si está habilitado el filtrado de versión de cliente, la capacidad de la aplicación cliente para tener acceso al sistema dependerá de las opciones configuradas en la directiva de versión de cliente correspondiente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando que se muestra en el ejemplo 1 crea una recopilación de opciones de configuración de versión de cliente para el sitio de Redmond. En este comando, el parámetro Enabled está definido como False; por lo tanto, el filtrado de clientes se deshabilita en el sitio Redmond.

    New-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## Ejemplo 2

En el ejemplo 2 se muestra cómo crear una recopilación de opciones de configuración de versión de cliente en la memoria, modificarla y, a continuación, convertir esas opciones de configuración virtuales en una recopilación de configuraciones real aplicada al sitio Redmond. Para ello, el primer comando utiliza el cmdlet **New-CsClientVersionConfiguration** y el parámetro InMemory para crear una recopilación de configuraciones solamente en la memoria con la identidad site:Redmond. Esta recopilación se almacena en una variable llamada $x y solo existe en la memoria: si finaliza la sesión de Windows PowerShell o se elimina la variable $x, estas opciones de configuración de versión de cliente desaparecerán y nunca se aplicarán al sitio Redmond.

En el comando 2, el valor de la propiedad DefaultAction de las opciones de configuración virtuales se define en Block. En el comando 3, se usa el cmdlet **Set-CsClientVersionConfiguration** para transformar la configuración virtual en una recopilación real de opciones de configuración de versión de cliente aplicada al sitio Redmond.

    $x = New-CsClientVersionConfiguration -Identity site:Redmond -InMemory
    $x.DefaultAction = "Block" 
    Set-CsClientVersionConfiguration -Instance $x

## Descripción detallada

Lync Server ofrece a los administradores bastante libertad para especificar el software cliente, y el número de versión de dicho software, que pueden usar los usuarios para conectarse al sistema. Por ejemplo, no hay ningún motivo técnico que requiera que los usuarios se conecten a Lync Server usando Lync; no hay ninguna limitación técnica que impida que los usuarios inicien sesión usando Microsoft Office Communicator 2007 R2.

Sin embargo es posible que, por motivos no técnicos, prefiera que los usuarios no inicien sesión mediante Office Communicator 2007 R2. Por ejemplo, Office Communicator 2007 R2 no admite todas las funciones y funcionalidades de Lync y, como consecuencia, los usuarios que inicien sesión con Office Communicator 2007 R2 tendrán una experiencia diferente que los que se conecten usando Lync. Esto puede provocar problemas para los usuarios, y también para el personal de asistencia técnica, que debe ofrecer asistencia para diferentes aplicaciones cliente.

Si esto supone un problema para su organización, puede poner en práctica el filtrado de versión de cliente para especificar qué aplicaciones cliente pueden usarse para iniciar sesión en Lync Server. Al instalar Lync Server, se instala y habilita un conjunto de opciones de configuración de versión de cliente. Esta configuración se usa para determinar si se habilita el filtrado de versión de cliente.

Además de las opciones de configuración globales, el cmdlet **New-CsClientVersionConfiguration** permite crear opciones de configuración de versión de cliente en el ámbito de sitio. Al aplicar opciones de configuración de versión de cliente en el ámbito de sitio, dichas opciones tienen preferencia sobre las globales. Por ejemplo, supongamos que habilita el filtrado de versión de cliente en el ámbito global y, a continuación, crea una recopilación independiente de opciones de configuración para el sitio Redmond, en la que el filtrado de versión está deshabilitado. En este caso, el filtrado de versión de cliente estará deshabilitado para todos los usuarios con cuentas en el sitio Redmond.

Sin embargo, tenga en cuenta que los usuarios anónimos solo se ven afectados por los la configuración global. Esto se debe a que no están asociados a un sitio.

La configuración de versión de cliente no es una función de seguridad. La tecnología se basa en la información que suministran las aplicaciones cliente y no intenta verificar si una aplicación es realmente la aplicación especificada, ni si el número de versión suministrado es el real.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **New-CsClientVersionConfiguration** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionConfiguration"}

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
<th>Requerido</th>
<th>Tipo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Requerido</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Representa el identificador único que se asignará a la nueva recopilación de configuraciones de versión de cliente. Como solo puede crear nuevas colecciones en el ámbito del sitio, la Identidad siempre será el prefijo &quot;site:&quot; seguido del nombre del sitio; por ejemplo &quot;site:Redmond&quot;. Tenga en cuenta que el comando anterior fallará si ya existe una recopilación de configuraciones con el valor de Identity site:Redmond.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Indica la acción que se llevará a cabo si un usuario intenta iniciar sesión desde una aplicación cliente cuyo número de versión no se encuentre en la directiva de versión de cliente correspondiente. El parámetro DefaultAction debe definirse en uno de estos valores:</p>
<p>Allow: la aplicación cliente podrá iniciar sesión.</p>
<p>AllowWithUrl: la aplicación cliente podrá iniciar sesión. Además, se mostrará al usuario un cuadro de mensaje con la dirección URL de una página web en la que el usuario puede descargar la aplicación cliente aprobada. La dirección URL de esta página web debe especificarse como el valor de la propiedad DefaultUrl.</p>
<p>Block: la aplicación cliente no podrá iniciar sesión.</p>
<p>BlockWithUrl: la aplicación cliente no podrá iniciar sesión. Sin embargo, en el mensaje de acceso denegado se mostrará la dirección URL de una página web en la que el usuario puede descargar una aplicación cliente aprobada. La dirección URL de esta página web debe especificarse como el valor de la propiedad DefaultUrl.</p>
<p>Esta propiedad se omitirá si la propiedad Enabled está definida en False. Si la propiedad Enabled está definida como False, no se realizará ningún tipo de filtrado de versión de cliente.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultURL</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Especifica la dirección URL de la página web en la que los usuarios pueden descargar una aplicación cliente aprobada. Si se especifica este valor y DefaultAction está definido como BlockWithUrl, esta dirección URL aparecerá en el cuadro de mensaje de acceso denegado cada vez que un usuario intente iniciar sesión desde una aplicación cliente no admitida.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica si el filtrado de versión de cliente está habilitado o deshabilitado. Si la propiedad Enabled está definida como True, el servidor comprobará el número de versión de cada aplicación cliente que intente iniciar sesión y permitirá o denegará el acceso de acuerdo con la directiva de versión de cliente correspondiente. Si la propiedad Enabled está definida como False, se permitirá iniciar sesión a cualquier aplicación cliente compatible.</p>
<p>El valor predeterminado es True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean irrecuperables y que puedan surgir al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
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

Ninguno. El cmdlet **New-CsClientVersionConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

Crea instancias nuevas del objeto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vea también

#### Otros recursos

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

