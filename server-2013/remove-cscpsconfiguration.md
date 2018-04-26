---
title: Remove-CsCpsConfiguration
TOCTitle: Remove-CsCpsConfiguration
ms:assetid: 546343e1-a2e4-4bc0-bf6d-c8ae9bb3e690
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398358(v=OCS.15)
ms:contentKeyID: 48275283
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCpsConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Quita una configuración del servicio de estacionamiento de llamadas existente. El estacionamiento de llamadas es un servicio que permite a un usuario "estacionar" una llamada de teléfono entrante. Al estacionar una llamada, se transfiere a un número de un intervalo u órbita especificados, y se pone automáticamente en espera. Cualquiera (no solo la persona que respondió a la llamada originalmente) puede continuar con la conversación desde cualquier teléfono marcando el número correspondiente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsCpsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se usa el cmdlet **Remove-CsCpsConfiguration** para eliminar la configuración del servicio de estacionamiento de llamadas con el valor de Identity site:Redmond1. Dado que las identidades son únicas, este comando solo eliminará una configuración.

    Remove-CsCpsConfiguration -Identity site:Redmond1

## EJEMPLO 2

En el ejemplo 2, se eliminan todas las configuraciones del servicio Estacionamiento de llamadas que se han definido en el ámbito de sitio. En primer lugar, el comando usa el cmdlet **Get-CsCpsConfiguration** y el parámetro Filter para devolver todas las configuraciones del servicio Estacionamiento de llamadas que se han definido en el ámbito de sitio. El carácter comodín site:\* garantiza que solo se devolverán las configuraciones cuyo parámetro Identity comience por el valor de cadena site:. A continuación, la colección filtrada se canaliza al cmdlet **Remove-CsCpsConfiguration**, que elimina los distintos elementos de la colección. Tenga en cuenta que, cada vez que quite la configuración del servicio Estacionamiento de llamadas de un sitio, este comenzará a usar automáticamente la configuración del servicio Estacionamiento de llamadas que se haya configurado en el ámbito global.

    Get-CsCpsConfiguration -Filter site:* | Remove-CsCpsConfiguration

## Descripción detallada

Este cmdlet se usa para quitar una configuración del servicio de estacionamiento de llamadas. Una configuración del servicio de estacionamiento de llamadas especifica qué sucede con una llamada después de estacionarla. Por ejemplo, si no se responde a una llamada estacionada en un período de tiempo, puede desviarse automáticamente a otra persona, como un administrador, o a un grupo de respuesta. Pueden configurarse las llamadas para que suene el teléfono pasado un período de tiempo para garantizar que no se olvidan. Además, el servicio de estacionamiento de llamadas se puede configurar para que la persona que está en espera escuche música mientras la llamada está estacionada.

Este cmdlet puede usarse para quitar cualquier configuración de estacionamiento de llamadas, incluida la configuración global. No obstante, en el caso de la configuración Global, no se quitará la configuración, sino que simplemente se restablecerá en los valores predeterminados.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsCpsConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCpsConfiguration"}

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
<td><p>Identificador único de la configuración del servicio de estacionamiento de llamadas que desea quitar. Este identificador será Global o site:&lt;nombre_sitio&gt;, donde &lt;nombre_sitio&gt; es el nombre del sitio al que se aplica la configuración.</p></td>
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
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Acepta entradas canalizadas de objetos de configuración del servicio de estacionamiento de llamadas.

## Tipos de valores devueltos

Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vea también

#### Otros recursos

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

