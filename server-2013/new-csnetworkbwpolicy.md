---
title: New-CsNetworkBWPolicy
TOCTitle: New-CsNetworkBWPolicy
ms:assetid: bbc91bd1-453c-4ae6-bb77-3b6be9429ed0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412916(v=OCS.15)
ms:contentKeyID: 48276485
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWPolicy

 

_**Última modificación del tema:** 2015-03-09_

Crea una directiva de ancho de banda en la memoria que se puede aplicar al perfil de directiva de ancho de banda. En Lync Server, la directiva se aplica al ancho de banda de audio y vídeo. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsNetworkBWPolicy -BWLimit <UInt32> -BWPolicyModality <Audio | Video> -BWSessionLimit <UInt32>

## Ejemplos

## Ejemplo 1

En este ejemplo se crea una directiva de ancho de banda y se asigna a la variable $bwp. Todos los parámetros del cmdlet **New-CsNetworkBWPolicy** son obligatorios. En este ejemplo, hemos especificado una cantidad límite total de ancho de banda (BWLimit) de 2000 kbps y un límite de sesión de ancho de banda (BWSessionLimit) de 300 kbps, y hemos aplicado estos límites a las sesiones de vídeo (-BWPolicyModality video).

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video

## Ejemplo 2

El ejemplo 2 amplía el ejemplo 1 asignando la nueva directiva de ancho de banda a un perfil de directiva. El comando de la línea 1 es idéntico al ejemplo 1: crea limitaciones de ancho de banda de vídeo. En la línea 2 se llama al cmdlet **New-CsNetworkBandwidthPolicyProfile** para agregar la directiva a un perfil nuevo. El nuevo perfil recibe una identidad de LowBWLimit. A continuación, se usa el parámetro BWPolicy, con el valor $bwp, que es la variable que contiene la nueva directiva de ancho de banda que acabamos de crear en la línea 1.

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video
    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bwp

## Descripción detallada

Este cmdlet crea una directiva de ancho de banda. Las directivas de ancho de banda se usan para definir las limitaciones de ancho de banda de determinadas modalidades. (En Lync Server, solo se pueden asignar limitaciones de ancho de banda a las modalidades de audio y vídeo). La directiva de ancho de banda se crea únicamente en la memoria, de modo que el resultado debe asignarse a una variable y, a continuación, enviarse como valor al parámetro BWPolicy del cmdlet **New-CsNetworkBandwidthPolicyProfile** o del cmdlet **Set-CsNetworkBandwidthPolicyProfile**. Las directivas de ancho de banda se aplican a los perfiles de directiva, que pueden almacenar varias directivas para un solo perfil y forman parte de la configuración de red global para el control de admisión de llamadas (CAC).

Tenga en cuenta que se recomienda asignar directivas de audio y vídeo directamente a un perfil de directiva de ancho de banda llamando al cmdlet **New-CsNetworkBandwidthPolicyProfile** o al cmdlet **Set-CsNetworkBandwidthPolicyProfile** y especificando valores para los parámetros AudioBWLimit, AudioBWSessionLimit, VideoBWLimit y VideoBWSessionLimit.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **New-CsNetworkBWPolicy** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWPolicy"}

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
<td><p><em>BWLimit</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.UInt32</p></td>
<td><p>La cantidad máxima total de ancho de banda, en kbps, para todas las sesiones simultáneas del tipo especificado en el parámetro BWPolicyModality.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
<td><p>Determina el tipo de ancho de banda que está limitado.</p>
<p>Valores válidos: Audio, Video</p></td>
</tr>
<tr class="odd">
<td><p><em>BWSessionLimit</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.UInt32</p></td>
<td><p>La cantidad máxima total de ancho de banda, en kbps, permitida para una sola sesión del tipo especificado en el parámetro BWPolicyModality.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Crea un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType.

## Vea también

#### Otros recursos

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

