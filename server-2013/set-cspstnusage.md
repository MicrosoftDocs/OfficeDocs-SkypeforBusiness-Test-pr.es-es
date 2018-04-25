---
title: Set-CsPstnUsage
TOCTitle: Set-CsPstnUsage
ms:assetid: ecba9ed6-4845-4035-933e-0c540d530b72
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399069(v=OCS.15)
ms:contentKeyID: 48277077
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnUsage

 

_**Última modificación del tema:** 2015-03-09_

Modifica un conjunto de cadenas de caracteres que identifican los usos permitidos de la red telefónica conmutada (RTC). Este cmdlet se puede utilizar para agregar usos a la lista de usos de RTC o quitar usos de la lista. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPstnUsage [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Usage <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este comando agrega la cadena de caracteres "International" a la lista actual de usos de RTC disponibles.

    Set-CsPstnUsage -Identity global -Usage @{add="International"}

## Ejemplo 2

Este comando quita la cadena de caracteres "Local" de la lista de usos de RTC disponibles.

    Set-CsPstnUsage -Identity global -Usage @{remove="Local"}

## Ejemplo 3

El comando de este ejemplo ejecuta la misma acción que el ejemplo 2: quita el uso de RTC "Local". Este ejemplo muestra el comando sin el parámetro Identity especificado. El único valor de Identity disponible para el cmdlet **Set-CsPstnUsage** es la identidad Global; si no se especifica el parámetro Identity, se usará la opción predeterminada Global.

    Set-CsPstnUsage -Usage @{remove="Local"}

## Ejemplo 4

Este comando reemplaza todos los valores de la lista de usos por los valores International y Restricted. Todos los usos anteriores se quitan.

    Set-CsPstnUsage -Usage @{replace="International","Restricted"}

## Descripción detallada

Los usos de RTC son valores de cadenas de caracteres que se usan para la autorización de llamadas. Un uso de RTC vincula una directiva de voz con una ruta. El cmdlet **Set-CsPstnUsage** se usa para agregar o quitar usos de teléfono de la lista de usos. Esta lista es global, pueden usarla tanto las directivas como las rutas de toda la implementación de Lync Server.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **Set-CsPstnUsage** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnUsage"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>El ámbito en el que se aplican estas configuraciones. La identidad de este cmdlet siempre es Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>PstnUsages</p></td>
<td><p>Una referencia a un objeto de uso de RTC. Este objeto debe ser de tipo PstnUsages y se puede recuperar llamando al cmdlet <strong>Get-CsPstnUsage</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Usage</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Contiene una lista de cadenas de caracteres de uso permitidas. Estas entradas pueden ser cualquier valor de cadena de caracteres.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages. Acepta la entrada por canalización de objetos de uso de RTC.

## Tipos de valores devueltos

Este cmdlet no devuelve un objeto o valor. Por el contrario, configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages.

## Vea también

#### Otros recursos

[Get-CsPstnUsage](get-cspstnusage.md)

