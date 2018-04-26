---
title: Get-CsConferenceDisclaimer
TOCTitle: Get-CsConferenceDisclaimer
ms:assetid: 2382aaef-9c5e-43f8-99de-6c880134db7d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425714(v=OCS.15)
ms:contentKeyID: 48274685
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDisclaimer

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre el aviso de declinación de responsabilidades de conferencias usado en la organización. El aviso de declinación de responsabilidades de conferencias es un mensaje que se muestra a los usuarios que se unen a la conferencia a través de un hipervínculo (por ejemplo, aquéllos que pegan un vínculo que lleva a la conferencia en un explorador como Windows Internet Explorer). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 devuelve información sobre el aviso de declinación de responsabilidades de conferencias configurado para ser utilizado en la organización. Como existe la limitación de un único aviso de declinación de responsabilidades (configurado en el ámbito global), no es necesario especificar una identidad al ejecutar este comando.

    Get-CSConferenceDisclaimer

## Descripción detallada

Al definir la configuración de las conferencias, los administradores pueden incluir un aviso de declinación de responsabilidades legales para que se muestre a los participantes cuando se unan a una conferencia hospedada por Lync Server. Este aviso de declinación de responsabilidades se suele usar para explicar las normas legales y de propiedad intelectual e industrial relacionadas con la conferencia y, si no aceptan las condiciones establecidas en él, los usuarios no podrán participar en la conferencia. Tenga en cuenta que este aviso de declinación de responsabilidades se muestra únicamente a los usuarios que se unen a la conferencia a través de un hipervínculo.

El cmdlet **Get-CsConferenceDisclaimer** permite ver el cuerpo y el encabezado del aviso de declinación de responsabilidades de la organización.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Get-CsConferenceDisclaimer** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDisclaimer"}

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
<td><p>Permite utilizar valores comodines al hacer referencia a un aviso de declinación de responsabilidades de conferencias. Como solo se puede tener una única instancia global del aviso de declinación de responsabilidades de conferencias, no existe ninguna razón para utilizar el parámetro Filter. Sin embargo, puede usar la siguiente sintaxis para hacer referencia al aviso de declinación de responsabilidades global: -Filter &quot;g*&quot;. La sintaxis devuelve todos los avisos de declinación de responsabilidades de conferencias que tienen una Identidad que empieza por la letra &quot;g&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identidad única del aviso de declinación de responsabilidades de conferencia. Como solo se puede tener una única instancia global del aviso de declinación de responsabilidades de conferencia, no es necesario especificar una identidad al llamar al cmdlet <strong>Get-CsConferenceDisclaimer</strong>. Sin embargo, puede usar la siguiente sintaxis para hacer referencia al aviso de declinación de responsabilidades global: -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de aviso de declinación de responsabilidades de conferencias a partir de una réplica local de Almacén de administración central en lugar de hacerlo directamente desde Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Get-CsConferenceDisclaimer** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Vea también

#### Otros recursos

[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

