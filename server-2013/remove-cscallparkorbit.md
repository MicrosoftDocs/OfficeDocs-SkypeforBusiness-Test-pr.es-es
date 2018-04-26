---
title: Remove-CsCallParkOrbit
TOCTitle: Remove-CsCallParkOrbit
ms:assetid: b8e7c236-f8de-45bd-966b-60c815b37aed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412901(v=OCS.15)
ms:contentKeyID: 48276474
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCallParkOrbit

 

_**Última modificación del tema:** 2015-03-09_

Quita un intervalo de órbitas de estacionamiento de llamadas específico. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo, se usa el cmdlet **Remove-CsCallParkOrbit** para eliminar el intervalo de órbitas de estacionamiento de llamadas con el nombre Redmond CPO 1.

    Remove-CsCallParkOrbit -Identity "Redmond CPO 1"

## Ejemplo 2

El comando de este ejemplo quita todos los intervalos de órbitas de estacionamiento de llamadas que se hayan definido para una organización. En primer lugar, el comando llama al cmdlet **Get-CsCallParkOrbit** sin ningún parámetro para recuperar todos los intervalos de órbitas de estacionamiento de llamadas definidos. A continuación, transfiere la colección de intervalos de órbitas de estacionamiento de llamadas al cmdlet **Remove-CsCallParkOrbit**, que quita todas las órbitas de estacionamiento de llamadas.

    Get-CsCallParkOrbit | Remove-CsCallParkOrbit

## Ejemplo 3

Este comando quita todos los intervalos de órbitas de estacionamiento de llamadas que tengan una identidad que incluya la cadena de caracteres "Redmond", como "Redmond 501", "CP Redmond 1" y "ARedmond". En primer lugar, el comando llama al cmdlet **Get-CsCallParkOrbit** con el parámetro Filter para recuperar todos los intervalos de órbitas de estacionamiento de llamadas con una identidad que contenga la cadena de caracteres Redmond. Esta colección se canaliza al cmdlet **Remove-CsCallParkOrbit**, que quita todo el contenido de la colección.

    Get-CsCallParkOrbit -Filter *Redmond* | Remove-CsCallParkOrbit

## Descripción detallada

El cmdlet **Remove-CsCallParkOrbit** elimina el intervalo de órbitas de estacionamiento de llamadas con el nombre que se ha enviado al parámetro Identity (este parámetro es obligatorio). Cada órbita de estacionamiento de llamadas de una organización debe tener un intervalo de números único. Al quitar una órbita de estacionamiento de llamadas, se libera el intervalo que había en la órbita de estacionamiento de llamadas. Los números liberados pueden usarse en una órbita de estacionamiento de llamadas recién definida.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Remove-CsCallParkOrbit** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCallParkOrbit"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nombre del intervalo de órbitas de estacionamiento de llamadas. Este nombre lo especifica el administrador al definir el intervalo de órbitas de estacionamiento de llamadas.</p></td>
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
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
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

Objeto Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit. Acepta la entrada canalizada de objetos de órbita de estacionamiento de llamadas.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor. Quita un objeto de tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit.

## Vea también

#### Otros recursos

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

