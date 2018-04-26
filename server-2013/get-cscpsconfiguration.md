---
title: Get-CsCpsConfiguration
TOCTitle: Get-CsCpsConfiguration
ms:assetid: d81ee8fe-d02b-4f60-a4d5-6aa84f65d156
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398948(v=OCS.15)
ms:contentKeyID: 48276841
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCpsConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre el servicio de estacionamiento de llamadas. El estacionamiento de llamadas es un servicio que permite a un usuario "estacionar" una llamada de teléfono entrante. Al estacionar una llamada, esta se transfiere a un número dentro de un intervalo u órbita especificados e, inmediatamente, la llamada se pone en espera. Cualquiera (no solo la persona que respondió a la llamada originalmente) puede continuar con la conversación desde cualquier teléfono marcando el número correcto. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCpsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

En el ejemplo 1 se recupera una colección de todas las configuraciones de servicio de estacionamiento de llamadas que se hayan definido para el uso en la organización.

    Get-CsCpsConfiguration

## Ejemplo 2

El comando anterior recupera solo las configuraciones del servicio de estacionamiento de llamadas con Identity site:Redmond1.

    Get-CsCpsConfiguration -Identity site:Redmond1

## Ejemplo 3

En el ejemplo 3, se usa el parámetro Filter para devolver todas las configuraciones del servicio de estacionamiento de llamadas que se hayan configurado en el ámbito del sitio. La cadena de caracteres comodín site:\* indica al cmdlet **Get-CsCpsConfiguration** que solo devuelva las configuraciones en las que la identidad comience por el valor de cadena site:.

    Get-CsCpsConfiguration -Filter site:*

## Ejemplo 4

Como en el ejemplo 3, en este ejemplo se usa el parámetro Filter para recuperar un subconjunto de todas las configuraciones de servicio de estacionamiento de llamadas definidas. En este caso, se filtra por la cadena \*:re\*, que devolverá configuraciones de estacionamiento de llamadas para todos los sitios que tengan nombres que comiencen por las letras "re", como Redmond1, Redmond2 y RemoteComputer.

    Get-CsCpsConfiguration -Filter *:re*

## Ejemplo 5

El comando anterior devuelve todas las configuraciones del servicio de estacionamiento de llamadas en las que no se reproduce música cuando se pone en espera al autor de una llamada. Para ello, el comando primero usa el cmdlet **Get-CsCpsConfiguration** para recuperar todas las configuraciones del servicio de estacionamiento de llamadas definidas para usarlas en la organización. A continuación, la colección se canaliza al cmdlet **Where-Object**, que aplica un filtro para restringir los datos que se devuelven a los elementos en los que la propiedad EnableMusicOnHold sea igual a (-eq) False.

    Get-CsCpsConfiguration | Where-Object {$_.EnableMusicOnHold -eq $False}

## Descripción detallada

Este cmdlet se usa para recuperar una o más configuraciones del servicio de estacionamiento de llamadas. Una configuración del servicio de estacionamiento de llamadas especifica qué sucede con una llamada cuando se ha estacionado. Por ejemplo, si no se responde a una llamada estacionada en un período de tiempo, puede desviarse automáticamente a otra persona, como un administrador, o a un grupo de respuesta. También pueden configurarse las llamadas para que suene el teléfono pasado un período de tiempo para garantizar que no se olvidan. Además, el servicio de estacionamiento de llamadas se puede configurar para que la persona que está en espera escuche música mientras la llamada está estacionada.

Quién puede ejecutar este cmdlet: de manera predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar localmente el cmdlet **Get-CsCpsConfiguration**: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluido cualquier otro rol RBAC personalizado que usted mismo haya creado), ejecute el siguiente comando desde Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCpsConfiguration"}

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
<td><p>Permite realizar una búsqueda con caracteres comodín para recuperar únicamente aquellas configuraciones con valores de identidad que coincidan con la cadena de caracteres comodín.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>El identificador único de la configuración del servicio de estacionamiento de llamadas que desea recuperar. Este identificador será Global o site:&lt;nombre_sitio&gt;, donde &lt;nombre_sitio&gt; es el nombre del sitio al que se aplica la configuración.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la información del servicio de estacionamiento de llamadas desde la réplica local del Almacén de administración central, en lugar de recuperarla del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Recupera uno o más objetos del tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vea también

#### Otros recursos

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

