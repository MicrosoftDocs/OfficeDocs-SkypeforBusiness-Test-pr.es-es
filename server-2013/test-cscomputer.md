---
title: Test-CsComputer
TOCTitle: Test-CsComputer
ms:assetid: 0b33d951-510d-445c-9b01-c6431fda6d47
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398162(v=OCS.15)
ms:contentKeyID: 48274388
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsComputer

 

_**Última modificación del tema:** 2015-03-09_

El cmdlet **Test-CsComputer** comprueba el estado de los servicios de Lync Server que se ejecutan en el equipo local. El cmdlet comprueba, además, que los grupos de Active Directory de Lync Server adecuados se hayan agregado a los grupos locales correspondientes del equipo y que se hayan abierto los puertos de firewall del equipo necesarios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsComputer [-Report <String>]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 comprueba el estado de activación del servicio en el equipo local. El parámetro -Verbose se incluye en el comando para asegurar que el resultado correcto (o con error) de la operación se informe en la pantalla de forma completa.

    Test-CsComputer -Verbose

## EJEMPLO 2

En el ejemplo 2 también se comprueba el estado de activación del servicio en el equipo local. Además, este comando escribe información detallada, acerca del estado de activación, en el archivo C:\\Logs\\Computer.html. Este registro se genera incluyendo el parámetro -Report seguido de la ruta de acceso completa del archivo de registro donde debería estar registrada la información.

    Test-CsComputer -Verbose -Report C:\Logs\Computer.html

## Descripción detallada

El cmdlet **Test-CsComputer** es un ejemplo de una "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la Red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

El cmdlet **Test-CsComputer**, que solo puede ejecutarse en el equipo local, comprueba el estado de todos los servicios de Lync Server en dicho equipo. El cmdlet comprueba, además, si se han abierto los puertos de firewall correctos en el equipo y determina si los grupos de Active Directory creados al instalar Lync Server se han agregado o no a los grupos locales correspondientes. Por ejemplo, el cmdlet **Test-CsComputer** comprueba si el grupo de Active Directory RTCUniversalUserAdmins se agregó al grupo de administradores locales.

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
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Le permite especificar una ruta de acceso para el archivo de registro creado cuando se ejecuta el cmdlet. Por ejemplo: -Report &quot;C:\Logs\Computer.html&quot;. Si el archivo ya existe, se sobrescribirá al ejecutar el cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsComputer** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsComputer** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)

