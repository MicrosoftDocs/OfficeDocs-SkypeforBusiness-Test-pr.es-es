---
title: Remove-CsClientVersionConfiguration
TOCTitle: Remove-CsClientVersionConfiguration
ms:assetid: 42065d1d-a0ef-4fa4-826b-d65b14b343c9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425925(v=OCS.15)
ms:contentKeyID: 48275098
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Quita la colección especificada de las opciones de configuración de la versión de cliente. Las opciones de configuración de la versión de cliente determinan si Lync Server comprueba o no el número de versión de cada aplicación cliente que se inicia en el sistema; si el filtrado de versión de cliente está habilitado, la capacidad de la aplicación cliente de obtener acceso al sistema se basará en la configuración definida en la directiva de versión de cliente adecuada. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

El comando que aparece en el ejemplo 1 elimina las opciones de configuración de versión de cliente que tienen Identity establecido en "site:Redmond".

    Remove-CsClientVersionConfiguration -Identity site:Redmond

## EJEMPLO 2

En el ejemplo 2 se eliminan todos los valores de configuración de versión de cliente que se han aplicado en el ámbito de sitio. En primer lugar, el comando llama al cmdlet **Get-CsClientVersionConfiguration** y al parámetro Filter. El valor de filtro "site:\*" garantiza que solo se devolverán los valores de configuración de versión de cliente cuyo parámetro Identity comience por el valor de cadena "site:". Seguidamente, la colección filtrada se canaliza al cmdlet **Remove-CsClientVersionConfiguration**, que elimina los distintos elementos de la colección.

    Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## EJEMPLO 3

En el ejemplo 3 se eliminan todos los valores de configuración de versión de cliente que actualmente se encuentran deshabilitados. En primer lugar, el comando usa el cmdlet **Get-CsClientVersionConfiguration** para devolver una colección con todos los valores de configuración de versión de cliente que actualmente se encuentran en uso en la organización. Tras devolver estos datos, la colección se canaliza al cmdlet **Where-Object**, que selecciona solo aquellos valores cuya propiedad Enabled es igual a False. Seguidamente, la colección filtrada se canaliza al cmdlet **Remove-CsClientVersionConfiguration**, que elimina los distintos elementos de la colección.

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionConfiguration

## Descripción detallada

Lync Server otorga a los administradores una libertad de acción considerable para especificar el software cliente (y, lo que es igual de importante, el número de versión de dicho software) que pueden utilizar los usuarios para iniciar la sesión en el sistema. Por ejemplo, no hay ningún motivo técnico que requiera que los usuarios inicien sesión en Lync Server usando Lync; desde un punto de vista técnico, no hay ninguna razón que impida que los usuarios inicien sesión usando Microsoft Office Communicator 2007 R2.

Con todo, puede haber otros motivos (no técnicos) por los que prefiera que los usuarios no inicien sesión mediante Office Communicator 2007 R2. Por ejemplo, Office Communicator 2007 R2 no admite todas las características y funciones de Lync y, como consecuencia, los usuarios que inicien sesión con Office Communicator 2007 R2 tendrán una experiencia diferente que los que lo hagan con Lync. Esto puede crearles dificultades; asimismo, también puede presentar problemas para el personal del servicio de asistencia técnica, que debe prestar soporte a varias aplicaciones cliente diferentes.

Si esto supone un problema para la organización, puede poner en práctica el filtrado de versión de cliente para especificar qué aplicaciones cliente se pueden usar para iniciar sesión en Lync Server. Al instalar Lync Server, se instala y habilita un conjunto de opciones de configuración de versión de cliente. Además de la configuración global, la configuración de versión de cliente también se puede aplicar en el ámbito de sitio.

Las configuraciones del sitio que cree se podrán eliminar más adelante con el cmdlet **Remove-CsClientVersionConfiguration**. Tenga en cuenta que también puede ejecutar el cmdlet **Remove-CsClientVersionConfiguration** con la configuración global, aunque esta configuración no se quitará. En su lugar, las propiedades globales se restablecerán a sus valores predeterminados.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsClientVersionConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionConfiguration"}

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
<td><p>Identificador único para la colección de opciones de configuración de versión de cliente que se va a quitar. Para quitar la colección global, use la siguiente sintaxis: -Identity global. (Tenga en cuenta que la configuración global no se quita realmente; en lugar de ello, se restablecen las propiedades globales a los valores predeterminados). Para quitar una recopilación de sitios, use una sintaxis similar a esta: -Identity site:Redmond. Tenga en cuenta que no puede usar caracteres comodín para especificar el valor de Identity.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration. El cmdlet **Remove-CsClientVersionConfiguration** acepta instancias canalizadas del objeto de configuración de versión de cliente.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet elimina instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vea también

#### Otros recursos

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

