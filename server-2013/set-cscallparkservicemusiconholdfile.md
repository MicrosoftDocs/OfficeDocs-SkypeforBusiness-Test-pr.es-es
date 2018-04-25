---
title: Set-CsCallParkServiceMusicOnHoldFile
TOCTitle: Set-CsCallParkServiceMusicOnHoldFile
ms:assetid: af5e7573-4bfd-47b1-a92b-83b06a537158
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412836(v=OCS.15)
ms:contentKeyID: 48276367
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkServiceMusicOnHoldFile

 

_**Última modificación del tema:** 2015-03-09_

Cambia el archivo de audio que escucharán los autores de llamadas que estén en espera en una llamada estacionada. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsCallParkServiceMusicOnHoldFile -Content <Byte[]> -Service <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se establece el archivo SoothingMusic.wma como el archivo de audio que se reproduce para los autores de llamadas que están estacionadas. La primera línea de este ejemplo es una llamada al cmdlet **Get-Content**. Este cmdlet simplemente lee el contenido de un archivo y lo asigna, en este caso, a la variable $a. Se pasa un valor 0 al parámetro ReadCount para que el cmdlet **Get-Content** lea todo el archivo de una vez (en lugar de intentar leerlo línea por línea; esto no se aplica a un archivo de audio). El parámetro Encoding se define en bytes. Dicho parámetro indica al cmdlet **Get-Content** que el contenido que queremos leer en la variable $a es una matriz de bytes en lugar de un archivo de audio en formato .wma.

En este ejemplo, es en la línea 2 donde realmente se asigna el archivo de audio. Se llama al cmdlet **Set-CsCallParkServiceMusicOnHoldFile** y se especifica el identificador de servicio donde se ejecuta el servicio de estacionamiento de llamadas. Luego, se envía el contenido del archivo de audio leído en la variable $a al parámetro Content. (Recuerde que el contenido debe estar en formato de bytes).

    $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
    Set-CsCallParkServiceMusicOnHoldFile -Service ApplicationServer:pool0.litwareinc.com -Content $a

## Descripción detallada

El estacionamiento de llamadas es un servicio que permite a un usuario "estacionar" una llamada de teléfono entrante. Al estacionar una llamada se transfiere a un número en un intervalo específico y se pone inmediatamente en espera. Según las opciones de configuración del servicio de estacionamiento de llamadas, la música en espera se puede reproducir mientras la llamada está estacionada. Use este cmdlet para cambiar el archivo de audio (música en espera) que se reproduce cuando el autor de una llamada estacionada está en espera.

La música en espera solo se reproduce si la propiedad EnableMusicOnHold del servicio de estacionamiento de llamadas se ha definido en True. Puede comprobar esta propiedad si llama al cmdlet **Get-CsCpsConfiguration**. Puede definir la propiedad al crear la configuración de estacionamiento de llamadas con el cmdlet **New-CsCpsConfiguration** o, una vez creada la configuración de estacionamiento de llamadas, con el cmdlet **Set-CsCpsConfiguration**. Esta propiedad está definida en True de forma predeterminada.

Lync Server incluye un archivo predeterminado del servicio de estacionamiento de llamadas para la música en espera. Si no asigna ningún archivo de audio, se usará el archivo predeterminado.

Los archivos de audio deben estar en el formato siguiente: Windows Media Audio 9, 44 kHz, 16 bits, Mono, CBR o 32 kbps.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsCallParkServiceMusicOnHoldFile** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkServiceMusicOnHoldFile"}

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
<td><p><em>Content</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>El contenido del archivo de audio en formato de bytes.</p>
<p>Use el cmdlet <strong>Get-Content</strong> para recuperar el contenido del archivo de audio en formato de bytes. (Para obtener más información, vea la sección de ejemplos de este tema).</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>El Id. del servicio en el que reside el servicio de estacionamiento de llamadas; por ejemplo, ApplicationServer:pool0.litwareinc.com.</p></td>
</tr>
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
<td><p>Suprime las preguntas de confirmación que aparecen antes de hacer cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Byte\[\]: acepta la entrada canalizada de una matriz de bytes que contiene el archivo de música en espera.

## Tipos de valores devueltos

Este cmdlet no devuelve ningún valor.

## Vea también

#### Otros recursos

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)

