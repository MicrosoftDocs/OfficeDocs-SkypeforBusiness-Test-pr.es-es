---
title: Set-CsRoutingConfiguration
TOCTitle: Set-CsRoutingConfiguration
ms:assetid: ab69c6e8-262a-4ecb-b1af-513383c494fe
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412811(v=OCS.15)
ms:contentKeyID: 48276325
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRoutingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica una lista de rutas de voz. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Para modificar una ruta de voz en una configuración de enrutamiento, se deben seguir varios pasos. En este ejemplo, comenzamos por recuperar el objeto de configuración de enrutamiento mediante el cmdlet **Get-CsRoutingConfiguration**. Luego, asignamos el objeto recuperado (solo habrá uno) a la variable $a.

En la línea 2 de este ejemplo, se recupera el contenido de la propiedad Route de la variable $a, que es una colección de objetos de rutas de voz. Después, la colección se canaliza al cmdlet **Where-Object**, donde se buscan todos los objetos de rutas de voz cuyo valor de Name coincida con la cadena de caracteres LocalRoute. El objeto se asigna a la variable $b.

A continuación, se modifica el objeto de ruta de voz LocalRoute al asignar el valor $False a la propiedad SuppressCallerId. Al actualizar el objeto, también se actualiza el objeto que se encuentra en la variable $a. Sin embargo, dicho objeto sigue estando únicamente en la memoria. El último paso consiste en guardar los cambios al enviar la variable $a al parámetro Instance del cmdlet **Set-CsRoutingConfiguration**.

Este no es el método recomendado para modificar una configuración de enrutamiento. Para modificar una configuración de enrutamiento, modifique cada una de las rutas de voz por separado con el cmdlet **Set-CsVoiceRoute**, como se muestra aquí:

Set-CsVoiceRoute -Identity LocalRoute -SuppressCallerId $False

Esta línea llevará a cabo la misma acción que se ha explicado en el ejemplo 1.

    $a = Get-CsRoutingConfiguration
    $b = $a.Route | Where-Object {$_.Name -match "LocalRoute"}
    $b.SuppressCallerId = $False
    Set-CsRoutingConfiguration -Instance $a

## Descripción detallada

Las rutas de voz contienen instrucciones que indican a Lync Server cómo enrutar las llamadas de usuarios de telefonía IP empresarial al número de teléfono de la red telefónica conmutada (RTC) o a una central de conmutación PBX. Con este cmdlet puede modificar la configuración de cualquier ruta de voz que esté definida en una instalación de Lync Server.

No se recomienda el uso de este cmdlet. Para modificar las configuraciones de enrutamiento, modifique las rutas de voz por separado llamando al cmdlet **Set-CsVoiceRoute**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsRoutingConfiguration** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRoutingConfiguration"}

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
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Cuando se establece como True, el enrutamiento de voz se administra teniendo en cuenta la ubicación tanto del usuario que realiza la llamada como del usuario que la recibe. El valor predeterminado es False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecen antes de hacer cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>El ámbito de la configuración de enrutamiento. Debe ser Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Objeto de configuración de enrutamiento (Microsoft.Rtc.Management.WritablConfig.Policy.Voice.PstnRoutingSettings). Un objeto de este tipo puede recuperarse con el cmdlet <strong>Get-CsRoutingConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de todos los enrutamientos de voz (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route objects) definidos para la instalación de Lync Server.</p>
<p>Para modificar los objetos de rutas de voz uno a uno, use el cmdlet <strong>Set-CsVoiceRoute</strong>. Se trata del método recomendado para modificar rutas de esta lista.</p></td>
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

Objeto Microsoft.Rtc.WritableConfig.Management.Policy.Voice.PSTNRoutingSettings. Acepta la entrada canalizada de un objeto de configuración de enrutamiento.

## Tipos de valores devueltos

El cmdlet **Set-CsRoutingConfiguration** no devuelve ningún valor ni objeto. En su lugar, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings.

## Vea también

#### Otros recursos

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

