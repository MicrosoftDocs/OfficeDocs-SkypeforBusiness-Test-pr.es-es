---
title: Remove-CsConferenceDisclaimer
TOCTitle: Remove-CsConferenceDisclaimer
ms:assetid: 196252a1-2526-4944-9064-01d1846f3266
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398243(v=OCS.15)
ms:contentKeyID: 48274572
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDisclaimer

 

_**Última modificación del tema:** 2015-03-09_

Borra el texto del encabezado y el cuerpo de la declinación de responsabilidades de conferencias utilizada en la organización. El aviso de declinación de responsabilidades de conferencias es un mensaje que se muestra a los usuarios que se unen a la conferencia a través de un hipervínculo (por ejemplo, aquéllos que pegan un vínculo que lleva a la conferencia en un explorador como Windows Internet Explorer). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsConferenceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se restablecen los valores de propiedad de la declinación de responsabilidades global. Esto significa que tanto el encabezado como el cuerpo de la declinación de responsabilidades se establecen en valores nulos, lo que dará lugar a una declinación de responsabilidades en blanco.

    Remove-CsConferenceDisclaimer -Identity global

## Descripción detallada

Al definir la configuración de las conferencias, los administradores pueden incluir un aviso de declinación de responsabilidades legales para que se muestre a los participantes cuando estos se unan a una conferencia hospedada por Lync Server. El aviso de declinación de responsabilidades se suele usar para explicar las normas legales y de propiedad intelectual e industrial relacionadas con la conferencia. Los usuarios no pueden participar en la conferencia sin aceptar las condiciones establecidas en el aviso de declinación de responsabilidades. Tenga en cuenta que este aviso de declinación de responsabilidades se muestra únicamente a los usuarios que se unen a la conferencia a través de un hipervínculo.

Lync Server permite usar únicamente un aviso de declinación de responsabilidades de conferencias global. El cmdlet **Remove-CsConferenceDisclaimer** permite restablecer el aviso de declinación de responsabilidades de conferencias: al ejecutar este cmdlet, tanto el encabezado como el cuerpo de la declinación de responsabilidades se establecen en valores nulos.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsConferenceDisclaimer** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDisclaimer"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identidad única del aviso de declinación de responsabilidades de conferencia que se va a quitar. A pesar de que solo puede tener una única instancia global del aviso de declinación de responsabilidades de conferencia, deberá seguir usando el parámetro Identity al llamar al cmdlet <strong>Remove-CsConferenceDisclaimer</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no son graves y que pueden surgir al ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer. El cmdlet **Remove-CsConferenceDisclaimer** acepta entradas canalizadas de objetos de aviso de declinación de responsabilidades de conferencia.

## Tipos de valores devueltos

Ninguno. En su lugar, el cmdlet **Remove-CsConferenceDisclaimer** restablece instancias existentes del objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer a los valores de propiedad predeterminados.

## Vea también

#### Otros recursos

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

