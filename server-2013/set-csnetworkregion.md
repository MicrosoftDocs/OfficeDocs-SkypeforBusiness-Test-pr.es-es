---
title: Set-CsNetworkRegion
TOCTitle: Set-CsNetworkRegion
ms:assetid: ffa1774b-ac60-4392-ad55-07bb887bf945
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg413089(v=OCS.15)
ms:contentKeyID: 48277286
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegion

 

_**Última modificación del tema:** 2015-03-09_

Modifica una región de red existente. Las regiones de red representan concentradores de red o redes troncales dentro de la red de una empresa. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-CentralSite <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se modifica la región de red denominada NorthAmerica. Se especifica el valor "North American Region" para el parámetro Description. Si ya existía una descripción en la región NorthAmerica, este comando la sobrescribirá con el nuevo valor. Si no se había definido ninguna descripción, el comando la definirá.

    Set-CsNetworkRegion -Identity NorthAmerica -Description "North American Region"

## Ejemplo 2

En este ejemplo, se modifica la región de red denominada EMEA y se especifica un nuevo valor de ruta de acceso de vídeo alternativa. Para ello, se llama al cmdlet **Set-CsNetworkRegion** y se le transfiere el valor de Identity EMEA. A continuación, se especifica el parámetro VideoAlternatePath, transfiriendo el valor $False. Al configurar VideoAlternatePath como False, se indica que, si el ancho de banda adecuado no está disponible, la llamada de vídeo no se redirigirá a una ruta de acceso alternativa y no se completará.

    Set-CsNetworkRegion -Identity EMEA -VideoAlternatePath $False

## Ejemplo 3

En el ejemplo 3 se asigna el mismo conjunto de opciones de ruta alternativa que se ha definido para la región NorthAmerica a la región de red Asia. En la primera línea del ejemplo se recupera una instancia de la región de red NorthAmerica y se asigna a la variable $a. En la segunda línea, se empieza recuperando el contenido de la propiedad BWAlternatePaths o de la región NorthAmerica (almacenado en la variable $a): $a.BWAlternatePaths. Se tratará de una recopilación de todas las opciones de ruta alternativa de la región NorthAmerica.

El siguiente paso consiste en canalizar la recopilación de configuraciones a la función foreach. Foreach pasará por cada uno de los elementos de la recopilación y realizará las acciones que se encuentran dentro de las sucesivas llaves. En este caso, la acción consiste en llamar al cmdlet **Set-CsNetworkRegion** con el valor de Identity Asia para establecer las propiedades de la región Asia. El parámetro siguiente es BWAlternatePaths. Transferimos el valor @{add=$\_} a este parámetro. La variable $\_ representa el elemento actual de la recopilación: en este caso, se trata de la ruta de acceso alternativa actual. La parte @{add=} del valor agrega el elemento a la recopilación de BWAlternatePaths de la región Asia.

    $a = Get-CsNetworkRegion -Identity NorthAmerica
    $a.BWAlternatePaths | foreach {Set-CsNetworkRegion -Identity Asia -BWAlternatePaths @{add=$_}}

## Descripción detallada

Una región de red interconecta varias partes de una red a través de varias zonas geográficas. Cada región de red debe estar asociada con un sitio central. El sitio central es el sitio del centro de datos donde se está ejecutando el servicio de directiva de ancho de banda de CAC (control de admisión de llamadas). Use este cmdlet para modificar una región de red existente, incluidas las opciones que determinan si están permitidas las rutas de acceso alternativas para las conexiones de audio y vídeo, y que asocian los sitios de la región con una configuración de omisión de medios.

Quién puede ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsNetworkRegion** de manera local: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC), se ha asignado este cmdlet (incluidos los roles RBAC que haya creado usted mismo) para ejecutar el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegion\\b"}

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
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Este parámetro determina si las llamadas de audio se enrutarán a través de una ruta de acceso alternativa si no existe ancho de banda adecuado en la ruta de acceso principal.</p>
<p>Este parámetro rellana la propiedad BWAlternatePaths. El valor proporcionado para este parámetro está almacenado en la propiedad AlternatePath para el elemento de ruta de acceso alternativa con el valor Audio para BWPolicyModality.</p>
<p>Si proporciona un valor para este parámetro, no podrá especificar ningún valor para el parámetro BWAlternatePaths.</p>
<p>Si alguna de las llamadas se realiza por Internet, este valor debe ser True, independientemente de la configuración de ancho de banda.</p></td>
</tr>
<tr class="even">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de objetos que contienen información sobre si están permitidas las rutas de conexión alternativas si no se puede completar una solicitud de medios con la ruta de acceso preferida (por ejemplo, si se han excedido los límites en la ruta de acceso en cuestión). Los objetos de ruta de acceso alternativa deben ser del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType. Puede crear objetos de este tipo llamando al cmdlet <strong>New-CsNetworkBWAlternatePath</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Un identificador único global (GUID). Este GUID se usa para asignar regiones de red a opciones de omisión de medios de una configuración de red CAC o E9-1-1 (9-1-1 mejorado). (Use este valor de BypassID para llamar al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>).</p>
<p>Este parámetro se puede generar automáticamente al crear la región (llamando al cmdlet <strong>New-CsNetworkRegion</strong>). No se recomienda cambiar este valor. Si especifica un valor, debe estar en el formato de un GUID (por ejemplo, 3b24a047-dce6-48b2-9f20-9fbff17ed62a). Recibirá una confirmación donde se le indicará que compruebe si realmente quiere definir este valor manualmente.</p></td>
</tr>
<tr class="even">
<td><p><em>CentralSite</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>El sitio central donde se ejecuta el servicio de directiva de ancho de banda. Este servicio debe habilitarse para usar el CAC. Este servicio se ejecuta en el Servidor front-end o el Servidor Standard Edition.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Una cadena de caracteres que describe la región. Este parámetro se puede usar para proporcionar una explicación más descriptiva sobre la utilidad de la región que puede expresarse mediante el valor de Identity por sí solo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>El identificador único de la región de red que quiere modificar. El valor de Identity tendrá el formato de una cadena de caracteres que identifica de forma única la región.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSObject</p></td>
<td><p>Una referencia a un objeto de región de red. Este objeto debe ser del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType y puede recuperarse llamando al cmdlet <strong>Get-CsNetworkRegion</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Este parámetro determina si las llamadas de vídeo se enrutarán a través de una ruta de acceso alternativa si no existe ancho de banda adecuado en la ruta de acceso principal.</p>
<p>Este parámetro rellana la propiedad BWAlternatePaths. El valor proporcionado para este parámetro está almacenado en la propiedad AlternatePath para el elemento de ruta de acceso alternativa con el valor Video para BWPolicyModality.</p>
<p>Si proporciona un valor para este parámetro, no podrá especificar ningún valor para el parámetro BWAlternatePaths.</p>
<p>Si alguna de las llamadas serán llamadas por Internet, este valor debe ser True, independientemente de la configuración de ancho de banda.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType. Acepta datos transferidos de objetos de región de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Modifica un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vea también

#### Otros recursos

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

