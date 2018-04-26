---
title: Remove-CsNetworkSite
TOCTitle: Remove-CsNetworkSite
ms:assetid: 07b543a6-3aa0-4fce-85f9-9ddc75d7b14f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398135(v=OCS.15)
ms:contentKeyID: 48274338
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSite

 

_**Última modificación del tema:** 2015-03-09_

Quita un sitio de red que ha sido definido para control de admisión de llamadas (CAC) o 9-1-1 mejorado (E9-1-1). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se quita el sitio cuyo parámetro es Identity Vancouver de la configuración de CAC o E9-1-1.

    Remove-CsNetworkSite -Identity Vancouver

## EJEMPLO 2

En el ejemplo 2 se quitan todos los sitios que usan el perfil de directiva de ancho de banda llamado LowBWProfile de la configuración CAC o E9-1-1. En este ejemplo, primero se llama al cmdlet **Get-CsNetworkSite** para que recupere todos los sitios de red. Esta recopilación de sitios luego se canaliza al cmdlet **Where-Object**, que la restringe a solo aquellos sitios cuyo BWPolicyProfileID es igual a (-eq) LowBWProfile. Después, la nueva recopilación se canaliza al cmdlet **Remove-CsNetworkSite** para que quite dichos sitios.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Remove-CsNetworkSite

## Descripción detallada

Los sitios de red son las oficinas o ubicaciones configuradas dentro de cada región de una implementación de E9-1-1 o CAC. Este cmdlet quita un sitio de la configuración CAC o E9-1-1.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Remove-CsNetworkSite** en forma local: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSite"}

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
<td><p>Identificador único del objeto de contacto que se quiere quitar. Los sitios se crean únicamente en el ámbito global, por lo que no es necesario especificar el ámbito. En lugar de ello, es necesario especificar solo el Id. del sitio.</p></td>
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
<td><p>Suprime las solicitudes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType. Acepta entradas canalizadas de los objetos de sitio de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Quita un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vea también

#### Otros recursos

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

