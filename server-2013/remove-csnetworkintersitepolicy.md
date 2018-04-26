---
title: Remove-CsNetworkInterSitePolicy
TOCTitle: Remove-CsNetworkInterSitePolicy
ms:assetid: daf1afc8-cce4-4192-8ba4-05d26817198e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398963(v=OCS.15)
ms:contentKeyID: 48276888
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterSitePolicy

 

_**Última modificación del tema:** 2015-03-09_

Quita una directiva entre sitios de red que define las limitaciones de ancho de banda entre sitios que están vinculados directamente en una configuración de control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsNetworkInterSitePolicy -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este ejemplo quita la directiva de sitio de red con la identidad Reno\_Portland.

    Remove-CsNetworkInterSitePolicy -Identity Reno_Portland

## Ejemplo 2

En el ejemplo 2, se quitan todas las directivas de sitio de red definidas en la configuración de CAC. Se empieza con una llamada al cmdlet **Get-CsNetworkInterSitePolicy** para recuperar una colección de todas las directivas de sitio de red. A continuación, la colección se canaliza al cmdlet **Remove-CsNetworkInterSitePolicy**, que quita cada elemento de la colección.

    Get-CsNetworkInterSitePolicy | Remove-CsNetworkInterSitePolicy

## Descripción detallada

Cuando los sitios de red comparten un vínculo directo, es posible definir limitaciones de ancho de banda para las conexiones de audio y vídeo entre ambos sitos. Este cmdlet quita una directiva de sitio de red que asocia una directiva de limitación de ancho de banda con dos sitios conectados directamente.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Remove-CsNetworkInterSitePolicy**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterSitePolicy"}

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
<td><p>Identificador único de la directiva de sitio de red que se quiere quitar. Las directivas de sitio de red se crean únicamente en el ámbito global, de modo que este identificador no necesita especificar ningún ámbito. En lugar de ello, contiene una cadena que es un nombre único que identifica la directiva de sitio.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType. Acepta entradas canalizadas de objetos de directiva entre sitios de red.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor. Quita un objeto del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Vea también

#### Otros recursos

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

