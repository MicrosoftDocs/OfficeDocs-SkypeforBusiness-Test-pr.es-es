---
title: Get-CsAudioConferencingProvider
TOCTitle: Get-CsAudioConferencingProvider
ms:assetid: 4632e9d0-aa87-459f-ad7e-27125c11da5b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994030(v=OCS.15)
ms:contentKeyID: 52061673
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioConferencingProvider

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los proveedores de audioconferencia autorizados para su uso en la organización. Los proveedores de audioconferencia son empresas externas que prestan servicios de conferencia a las organizaciones.

El cmdlet **Get-CsAudioConferencingProvider** solo se puede usar con Microsoft Lync Online.

## Sintaxis

    Get-CsAudioConferencingProvider [[-Identity] <XdsGlobalRelativeIdentity>] [-LocalStore][<CommonParameters>]Get-CsAudioConferencingProvider [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Ejemplos

## Ejemplo 1

El comando que se muestra en el ejemplo 1 devuelve información sobre todos los proveedores de audioconferencia disponibles para su uso en la organización.

    Get-CsAudioConferencingProvider

## Ejemplo 2

En el ejemplo 2, se devuelve información sobre un solo proveedor de audioconferencia: el proveedor con la identidad Fabrikam Telecom.

    Get-CsAudioConferencingProvider -Identity "Fabrikam Telecom"

## Ejemplo 3

En el ejemplo 3, se ve cómo los valores de carácter comodín (y el parámetro Filter) se pueden usar para devolver información sobre los proveedores de audioconferencia. En este ejemplo, el valor de filtro "\*Fabrikam\*" devuelve todos los proveedores de audioconferencia que tienen el valor de cadena "Fabrikam" en cualquier lugar de su identidad.

    Get-CsAudioConferencingProvider -Filter "*Fabrikam*"

## Descripción detallada

Un proveedor de audioconferencia es una compañía de terceros que proporciona servicios de conferencia a las organizaciones. Entre otras cosas, los proveedores de audioconferencia ofrecen la posibilidad de que los usuarios puedan participar en la parte de audio de una conferencia o reunión sin estar en la oficina y sin estar conectados a la red corporativa ni Internet. Los proveedores de audioconferencia suelen proporcionar servicios de gama alta, como traducción en directo, transcripción y servicio de operador por conferencia en directo.

Cuando las organizaciones contratan a un proveedor de audioconferencia, los usuarios se pueden asignar al proveedor usando el cmdlet **Set-CsUserAcp**. Los administradores pueden recuperar información sobre los proveedores de audioconferencia que hay disponibles usando el cmdlet **Get-CsAudioConferencingProvider**.

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
<td><p>Le permite usar caracteres comodín cuando se indica que se devuelva el proveedor (o los proveedores) de audioconferencia. Por ejemplo, esta sintaxis devuelve información sobre todos los proveedores de audioconferencia que tienen el valor de cadena &quot;fabrikam&quot; en alguna parte de su identidad:</p>
<p>-Filter &quot;*fabrikam*&quot;</p>
<p>El parámetro Filter y el parámetro Identity no se pueden usar en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador único para el proveedor de audioconferencia que se va a devolver. Por ejemplo:</p>
<p>-Identity &quot;Fabrikam Telecom&quot;</p>
<p>En caso de que ni el parámetro Identity ni el parámetro Filter estén incluidos en un comando, el cmdlet <strong>Get-CsAudioConferencingProvider</strong> devuelve información sobre todos los proveedores disponibles.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos del proveedor de audioconferencia a partir de la réplica local del Almacén de administración central en lugar de hacerlo a partir del propio almacén.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsAudioConferencingProvider** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsAudioConferencingProvider** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.AudioConferencingProvider.AudioConferencingProvider\#Decorated.

## Vea también

#### Otros recursos

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

