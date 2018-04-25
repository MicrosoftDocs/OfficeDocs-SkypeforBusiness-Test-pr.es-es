---
title: Get-CsVoiceRoute
TOCTitle: Get-CsVoiceRoute
ms:assetid: 422abb2d-bff3-4b9a-b18c-d8202b01f69b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425926(v=OCS.15)
ms:contentKeyID: 48275042
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoute

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre las rutas de voz configuradas en una organización. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

Recupera las propiedades de todas las rutas de voz definidas en la organización.

    Get-CsVoiceRoute

## EJEMPLO 2

Recupera las propiedades de la ruta de voz Route1.

    Get-CsVoiceRoute -Identity Route1

## EJEMPLO 3

Este comando muestra las configuraciones de ruta de voz en las que la propiedad Identity contiene la cadena de caracteres "test" en cualquier ubicación dentro del valor. Para buscar el texto "test" solamente al final de la propiedad Identity, use el valor \*test. Para buscar el texto "test" solamente cuando aparece al principio de la propiedad Identity, especifique el valor test\*.

    Get-CsVoiceRoute -Filter *test*

## EJEMPLO 4

Este comando recupera todas las rutas de voz a las que no se ha asignado ninguna puerta de enlace RTC. En primer lugar, se recuperan todas las rutas de voz con el cmdlet **Get-CsVoiceRoute**. A continuación, estas rutas de voz se canalizan al cmdlet **Where-Object**. El cmdlet **Where-Object** restringe los resultados de la operación Get. En este caso, se examina cada ruta de voz (es lo que representa $\_) y se comprueba la propiedad Count de la propiedad PstnGatewayList. Si el número de puertas de enlace RTC es 0, la lista aparece vacía y significa que no se han definido puertas de enlace para la ruta.

    Get-CsVoiceRoute | Where-Object {$_.PstnGatewayList.Count -eq 0}

## Descripción detallada

Use este cmdlet para recuperar una o varias rutas de voz configuradas. Las rutas de voz contienen instrucciones que indican a Lync Server cómo enrutar las llamadas de usuarios de Telefonía IP empresarial a números de teléfono de la Red Telefónica Conmutada (RTC) o una central de conmutación PBX.

Este cmdlet se puede usar para recuperar información acerca de las rutas de voz, como con qué puertas de enlace RTC está asociada la ruta (si las hay), qué usos de RTC están relacionados con la ruta, el patrón (en forma de expresión regular) que identifica los números de teléfono a los que se aplica la ruta y la configuración del identificador del autor de llamada. El uso de RTC asocia la ruta de voz con una directiva de voz.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Get-CsVoiceRoute** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoute"}

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
<td><p>Este parámetro filtra los resultados de la operación Get según el valor de comodín enviado al parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Cadena de caracteres que identifica de manera única la ruta de voz. Si no se especifica una identidad, se devolverán todas las rutas de voz de la organización.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la ruta de voz a partir de una réplica local de Almacén de administración central en lugar de hacerlo directamente desde Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Este cmdlet devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Vea también

#### Otros recursos

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

