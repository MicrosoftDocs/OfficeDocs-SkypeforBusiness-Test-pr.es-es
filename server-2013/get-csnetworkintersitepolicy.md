---
title: Get-CsNetworkInterSitePolicy
TOCTitle: Get-CsNetworkInterSitePolicy
ms:assetid: a4a64048-f8d7-483a-9565-0c6f3b0937b7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412769(v=OCS.15)
ms:contentKeyID: 48276187
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterSitePolicy

 

_**Última modificación del tema:** 2015-03-09_

Recupera una o varias directivas de entre sitios de red que definen limitaciones de ancho de banda entre sitios enlazados directamente dentro de una configuración de control de admisión de llamadas (CAC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterSitePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

Si se llama al cmdlet **Get-CsNetworkInterSitePolicy** sin parámetros, se recuperan todas las directivas de sitio de red definidas entre dos sitios de red directamente vinculados.

    Get-CsNetworkInterSitePolicy

## Ejemplo 2

En este ejemplo se recupera la directiva de sitio de red con identidad Reno\_Portland.

    Get-CsNetworkInterSitePolicy -Identity Reno_Portland

## Ejemplo 3

En el ejemplo 3 se recuperan todas las directivas de sitio de red con la cadena de caracteres Reno en cualquier lugar del valor Identity. Los caracteres comodín (\*) dentro del valor, transferidos al parámetro Filter, significan “cualquier carácter o conjunto de caracteres”. Dicho de otro modo, la cadena de caracteres \*Reno\* coincide con los valores Identity que empiezan por cualquier carácter (uno o varios) y la cadena Reno a continuación, seguida de nuevo de uno o varios caracteres.

    Get-CsNetworkInterSitePolicy -Filter *Reno*

## Ejemplo 4

En este ejemplo se recuperan todas las directivas de sitio de red que no tienen asignado ningún perfil de directiva de ancho de banda. Para empezar, el comando llama al cmdlet **Get-CsNetworkInterSitePolicy** que, como hemos visto en el ejemplo 1, recupera una colección de todas las directivas de sitio de red. Después, la colección se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** reduce la colección únicamente a las directivas de sitio que no tengan asignado ningún perfil de directiva de ancho de banda. Para ello, comprueba si la propiedad BWPolicyProfileID de cada directiva de sitio es igual a (-eq) Null ($null) mediante una comparación.

    Get-CsNetworkInterSitePolicy | Where-Object {$_.BWPolicyProfileID -eq $null}

## Descripción detallada

Cuando los sitios de red comparten un vínculo directo, se pueden definir las limitaciones de ancho de banda de las conexiones de audio y vídeo entre ambos sitios. Este cmdlet recupera una o varias directivas de centro de red que asocian opciones de configuración de limitación de ancho de banda con sitios conectados directamente.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Get-CsNetworkInterSitePolicy** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterSitePolicy"}

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
<td><p>Cadena que contiene caracteres comodín para buscar directivas con valores de identidad que coincidan con la cadena comodín.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificador único de la directiva de sitio de red que se desea recuperar. Dado que las directivas de sitios de red se crean únicamente en el ámbito global, este identificador no necesita especificar el ámbito. Por el contrario, contiene una cadena que consiste en un nombre único que identifica la directiva.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información de la directiva de entre sitios de red de la réplica local de Almacén de administración central en lugar de hacerlo directamente de Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Recupera un objeto del tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Vea también

#### Otros recursos

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)

