---
title: New-CsNetworkBWAlternatePath
TOCTitle: New-CsNetworkBWAlternatePath
ms:assetid: 9017378e-4583-42bc-9572-aa8e9571cfe3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398732(v=OCS.15)
ms:contentKeyID: 48276009
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWAlternatePath

 

_**Última modificación del tema:** 2015-03-09_

Crea nuevas configuraciones que definen si los medios se pueden enrutar a rutas de acceso de Internet alternativas para las conexiones con ancho de banda limitado. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsNetworkBWAlternatePath -AlternatePath <$true | $false> -BWPolicyModality <Audio | Video>

## Ejemplos

## Ejemplo 1

En este ejemplo se crea una nueva ruta de acceso alternativa de ancho de banda de red y se asigna la configuración a una región recién creada. En la primera línea del ejemplo se llama al cmdlet **New-CsNetworkBWAlternatePath** para crear una nueva ruta de acceso alternativa. Las rutas de acceso alternativas tienen solo dos propiedades: BWPolicyModality, que debe configurarse como audio o vídeo (en este ejemplo se utiliza audio); y AlternatePath, que debe tener el valor True o False (True, en este ejemplo). Asignamos el resultado de este cmdlet, que es una referencia al objeto de ruta de acceso alternativa que se acaba de crear, a la variable $a.

En la línea 2 de este ejemplo, se usa la ruta de acceso alternativa recién creada para crear una nueva región de red. Para ello, llamamos al cmdlet **New-CsNetworkRegion** y pasamos la identidad NorthAmerica. Asignamos un valor al parámetro obligatorio CentralSite (en este ejemplo, el nombre del sitio central de esta región es Redmond-NA-MLS) y luego especificamos el parámetro BWAlternatePaths y le pasamos la variable ($a) que contiene el objeto de ruta de acceso alternativa que acabamos de crear.

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $true
    New-CsNetworkRegion -Identity NorthAmerica -CentralSite Redmond-NA-MLS -BWAlternatePaths $a

## Descripción detallada

Dentro de una configuración de control de admisión de llamadas (CAC) en Lync Server, hay dos modalidades posibles: audio y vídeo. Se pueden establecer limitaciones de ancho de banda en ambas modalidades. Si las limitaciones de ancho de banda impiden que se realice una llamada, dicha llamada puede tomar una ruta de acceso de Internet alternativa para que la llamada sea posible. Este cmdlet permite crear las configuraciones que definen si una llamada se puede enrutar a una ruta de acceso de Internet alternativa según su modalidad. Las configuraciones se aplican por región dentro de la configuración de CAC.

Este cmdlet no guarda inmediatamente las configuraciones recién creadas. Por el contrario, crea las configuraciones en la memoria. Para aplicar las configuraciones a una región de la red, debe asignar el resultado del cmdlet a una variable y luego usar la variable como valor para el parámetro BWAlternatePaths del cmdlet **New-CsNetworkRegion** o **Set-CsNetworkRegion**. Tenga en cuenta que puede aplicar las configuraciones directamente con los parámetros AudioAlternatePath y VideoAlternatePath de los cmdlets **New-CsNetworkRegion** y **Set-CsNetworkRegion**, sin necesidad de llamar al cmdlet **New-CsNetworkBWAlternatePath** para crear un nuevo objeto.

Quién puede iniciar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a iniciar localmente el cmdlet **New-CsNetworkBWAlternatePath**: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWAlternatePath"}

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
<td><p><em>AlternatePath</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Booleano</p></td>
<td><p>Asigne el valor True al parámetro para permitir que las llamadas hechas en el medio de la modalidad especificada en el parámetro BWPolicyModality (audio o vídeo) se enruten a una ruta de acceso alternativa si el ancho de banda necesario no existe en la ruta de acceso principal.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>BWPolicyModality</p></td>
<td><p>La modalidad a la que se aplica la configuración de ruta de acceso alternativa.</p>
<p>Valores válidos: audio, video</p>
<p>Tipo de datos completo: Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Crea un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType.

## Vea también

#### Otros recursos

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

