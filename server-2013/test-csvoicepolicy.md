---
title: Test-CsVoicePolicy
TOCTitle: Test-CsVoicePolicy
ms:assetid: 4d631e36-3a9d-4ca2-913f-8c9f4e93183d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398310(v=OCS.15)
ms:contentKeyID: 48275227
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoicePolicy

 

_**Última modificación del tema:** 2015-03-09_

Comprueba un número telefónico con una directiva de voz y determina qué ruta de voz se usará con esa directiva para ese número. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsVoicePolicy -TargetNumber <PhoneNumber> -VoicePolicy <VoicePolicy> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se realiza una prueba de directiva de voz con la directiva de voz con el valor de Identity site:Redmond. En primer lugar, se ejecuta el cmdlet **Get-CsVoicePolicy** para recuperar la directiva con el parámetro Identity site:Redmond. A continuación, este objeto de directiva se redirecciona al cmdlet **Test-CsVoicePolicy**, en el que la directiva se comprueba con el número telefónico +14255559999. El resultado será la primera ruta de voz (basada en la propiedad Priority de la ruta) que tenga el patrón numérico que coincida con el valor TargetNumber y el uso del teléfono que coincida con el uso del teléfono en la directiva. Si no se encuentra una ruta coincidente (por ejemplo, si el patrón numérico coincide con el patrón de un número de 11 dígitos y usted provee un número de 7 dígitos) el valor devuelto será nulo.

    Get-CsVoicePolicy -Identity site:Redmond | Test-CsVoicePolicy -TargetNumber "+14255559999"

## EJEMPLO 2

El ejemplo 2 es idéntico al ejemplo 1, aunque en lugar de canalizar los resultados de la operación Get directamente al cmdlet **Test-CsVoicePolicy**, en primer lugar se almacena el objeto en la variable $a y, a continuación, se transfiere como valor al parámetro VoicePolicy para usarse como directiva de la prueba.

    $a = Get-CsVoicePolicy -Identity site:Redmond
    Test-CsVoicePolicy -TargetNumber "+14255559999" -VoicePolicy $a

## EJEMPLO 3

En este ejemplo, se realiza una prueba de directiva de voz con todas las directivas de voz definidas en la instalación de Lync Server. En primer lugar, se ejecuta el cmdlet **Get-CsVoicePolicy** (sin parámetros) para recuperar todas las directivas de voz. La recopilación de directivas que se devuelve se redirecciona al cmdlet **Test-CsVoicePolicy**, en el que cada directiva de la recopilación se comprueba para ver si hay una ruta que coincida basada en el número de teléfono de destino proporcionado (+12065559999) y en los usos del teléfono. El resultado será una lista de rutas coincidentes junto con los usos del teléfono que coincidieron.

    Get-CsVoicePolicy | Test-CsVoicePolicy -TargetNumber "+12065559999"

## Descripción detallada

Las directivas de voz se asocian con las rutas de voz mediante los usos de la red telefónica conmutada (RTC). Una llamada de un usuario al que se le asignó una directiva de voz particular solo se puede enviar a través de la ruta que tiene un uso de RTC que coincida con un uso en la directiva y un patrón numérico que coincida con el número marcado. Llame al cmdlet **Test-CsVoicePolicy** para determinar qué ruta se usará (si hay alguna) para enrutar la llamada de un usuario con una directiva de voz particular y también cuál es el uso del teléfono que vincula la directiva con la ruta.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar el cmdlet **Test-CsVoicePolicy** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoicePolicy"}

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
<td><p><em>TargetNumber</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PhoneNumber</p></td>
<td><p>El número de teléfono con el que se realiza la prueba. Este número debe tener un formato E.164 (como +14255551212).</p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Una referencia a un objeto de directiva de voz para ejecutar la prueba. Los objetos de directiva de voz pueden recuperarse mediante el llamado del cmdlet <strong>Get-CsVoicePolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación o los mensajes de error que no sean graves que puedan surgir al ejecutar el cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>Opcional</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Configuración de la ruta con la que se debe realizar la prueba. La configuración de ruta se puede recuperar por medio del llamado del cmdlet <strong>Get-CsRoutingConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Acepta entradas canalizadas de objetos de directivas de voz.

## Tipos de valores devueltos

Devuelve un objeto de tipo Microsoft.Rtc.Management.Voice.VoicePolicyTestResult.

## Vea también

#### Otros recursos

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)

