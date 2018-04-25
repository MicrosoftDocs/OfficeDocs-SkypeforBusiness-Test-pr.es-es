---
title: Test-CsDialPlan
TOCTitle: Test-CsDialPlan
ms:assetid: e6618394-82c5-4bc2-85cc-97ac4686a1aa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399024(v=OCS.15)
ms:contentKeyID: 48276988
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialPlan

 

_**Última modificación del tema:** 2015-03-09_

Prueba un número de teléfono con un plan de marcado (antes denominado perfil de ubicación) y devuelve la regla de normalización que se aplicará al número, así como el número traducido después de haber aplicado la regla de normalización. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsDialPlan -DialedNumber <PhoneNumber> -Dialplan <LocationProfile>

## Ejemplos

## Ejemplo 1

En este ejemplo se realiza una prueba con el plan de marcado con el valor de Identity site:Redmond. En primer lugar se ejecuta el cmdlet **Get-CsDialPlan** para recuperar el plan de marcado con el valor de Identity site:Redmond. A continuación, el objeto de plan de marcado se transfiere al cmdlet **Test-CsDialPlan**, donde el plan de marcado se prueba con el número de teléfono 14255559999. El resultado será DialedNumber, después de la aplicación de una regla de normalización de voz con un patrón de coincidencia. Si hay más de una regla de normalización con un patrón de coincidencia en el sitio, se aplicará la regla que presente el valor de Priority más bajo. Si no hay ninguna regla con patrones que coincidan con el valor de DialedNumber (por ejemplo, si la regla de normalización coincide con el patrón por un número de 11 dígitos y usted proporciona un número de 7 dígitos), no se devolverá ningún valor.

El resultado de este comando incluye un número de teléfono y una regla de normalización. La regla de normalización tiene varias propiedades y, de forma predeterminada, el resultado quedará cortado por puntos suspensivos (...). Para ver todas las propiedades y los valores de la regla de normalización de voz devuelta, el resultado se transfiere al cmdlet **Format-List** antes de mostrarlo en la pantalla. El número de teléfono y la regla de normalización se mostrarán en líneas separadas, y las propiedades y los valores de la regla de normalización se ajustarán para que quepan en la pantalla.

    Get-CsDialPlan -Identity site:Redmond | Test-CsDialPlan -DialedNumber 14255559999 | Format-List

## Ejemplo 2

El Ejemplo 2 es idéntico al Ejemplo 1 con una diferencia: en lugar de transferir los resultados de la operación Get directamente al cmdlet **Test-CsDialPlan**, el objeto se almacena primero en la variable $a y después se transfiere como el valor al parámetro Dialplan para usarlo como el plan de marcado de la prueba.

Como en el ejemplo 1, este comando se finaliza canalizando el resultado al cmdlet **Format-List** para poder ver más información sobre la regla de normalización de voz que aparece de forma predeterminada.

    $a = Get-CsDialPlan -Identity site:Redmond
    Test-CsDialPlan -DialedNumber 14255559999 -Dialplan $a | Format-List

## Ejemplo 3

En este ejemplo se realiza una prueba de plan de marcado con todos los planes de marcado definidos en la instalación de Lync Server. Primero se ejecuta el cmdlet **Get-CsDialPlan** (sin parámetros) para recuperar todos los planes de marcado. A continuación, la colección de planes de marcado devuelta se transfiere al cmdlet **Test-CsDialPlan**, donde se prueban todos los planes de marcado de la colección con el número de teléfono 2065559999. El resultado será una lista de números traducidos junto con la regla de normalización de voz aplicada, una para cada plan de marcado de la colección. Si no se aplica ninguna regla de normalización de voz en un plan de marcado al valor de DialedNumber para un determinado plan de marcado (por ejemplo, si la regla de normalización coincide con el patrón por un número de 11 dígitos y usted proporciona un número de 7 dígitos), habrá una línea en blanco en la lista de dicho plan de marcado.

De forma predeterminada, el resultado corta la visualización completa de la regla de normalización de voz aplicada. En los Ejemplos 1 y 2 podíamos ver el resultado completo canalizando los resultados de la prueba al cmdlet **Format-List**. En este ejemplo, se canaliza el resultado al cmdlet **Format-Table** y se incluye el parámetro Wrap. De esta forma, se muestran todas las entradas en formato de tabla (una columna para el número traducido y otra para la regla de normalización de voz aplicada), pero se ajusta el resultado, de modo que la regla de normalización se ajustará a la columna.

    Get-CsDialPlan | Test-CsDialPlan -DialedNumber 2065559999 | Format-Table -Wrap

## Descripción detallada

Este cmdlet permite ver los resultados de la aplicación de un plan de marcado a un determinado número de teléfono. Los planes de marcado proporcionan información, como la forma en que se aplican las reglas de normalización, necesaria para habilitar las llamadas telefónicas para los usuarios de Telefonía IP empresarial. Después de especificar un número de marcado y un plan de marcado, el cmdlet verificará qué regla de normalización del plan de marcado se aplicará y cuál será el número traducido.

Puede usar este cmdlet para solucionar problemas con las traducciones de números o para verificar la aplicación de las reglas con determinados números.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **Test-CsDialPlan** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialPlan"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Requerido</p></td>
<td><p>PhoneNumber</p></td>
<td><p>El número de teléfono con el que quiera probar el plan de marcado especificado en el parámetro Dialplan.</p>
<p>Tipo de datos completo: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>Requerido</p></td>
<td><p>LocationProfile</p></td>
<td><p>Un objeto que contiene una referencia a un plan de marcado con el que quiere probar el número especificado en el parámetro DialedNumber.</p>
<p>Tipo de datos completo: Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile. Acepta la entrada por canalización de objetos de planes de marcado.

## Tipos de valores devueltos

Devuelve un objeto de tipo Microsoft.Rtc.Management.Voice.LocationProfileTestResult.

## Vea también

#### Otros recursos

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)

