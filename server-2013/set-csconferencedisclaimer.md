---
title: Set-CsConferenceDisclaimer
TOCTitle: Set-CsConferenceDisclaimer
ms:assetid: 97afce6d-b031-466d-a170-3ca50d6df245
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398776(v=OCS.15)
ms:contentKeyID: 48276097
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceDisclaimer

 

_**Última modificación del tema:** 2015-03-09_

Modifica los valores de propiedad del aviso de declinación de responsabilidades de conferencias que se usa en la organización. La declinación de responsabilidades de conferencia es un mensaje que se muestra a los usuarios que se unen a una conferencia con un hipervínculo (por ejemplo, al pegar un vínculo a la conferencia dentro de un explorador, como puede ser Windows Internet Explorer). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferenceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Header <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 modifica las propiedades Header y Body de la declinación de responsabilidades de conferencias de su organización. Dado que solo se puede tener una declinación de responsabilidades de este tipo, no es necesario especificar la identidad al ejecutar el cmdlet **Set-CsConferenceDisclaimer**.

    Set-CsConferenceDisclaimer -Header "Litwareinc.com Online Conference" -Body "Important note: Conferencing proceedings are recorded and archived."

## Descripción detallada

Al definir la configuración de las conferencias, los administradores pueden incluir una declinación de responsabilidades legales para que se muestre a los participantes cuando se unan a conferencias hospedadas por Lync Server. El aviso de declinación de responsabilidades se suele usar para explicar las normas legales y de propiedad intelectual e industrial relacionadas con la conferencia. Los usuarios no pueden participar en la conferencia sin aceptar las condiciones establecidas en la declinación de responsabilidades. No obstante, la declinación solamente se muestra a los usuarios que se unen a una conferencia con un hipervínculo.

Lync Server permite usar únicamente una declinación de responsabilidades de conferencia global. El cmdlet **Set-CsConferenceDisclaimer** permite modificar la declinación de responsabilidades de conferencia que se usa en la organización.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsConferenceDisclaimer** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Contenido del aviso de declinación de responsabilidades de conferencias.</p></td>
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
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Header</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Título del aviso de declinación de responsabilidades de conferencias.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identidad única del aviso de declinación de responsabilidades de conferencias. Dado que solo puede tener una instancia global de la declinación de responsabilidades de conferencia, no necesita especificar ninguna identidad al llamar al cmdlet <strong>Set-CsConferenceDisclaimer</strong>. Sin embargo, puede usar la siguiente sintaxis para hacer referencia a la declinación de responsabilidades global: -Identity global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>Objeto ConferenceDisclaimer</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer. El cmdlet **Set-CsConferenceDisclaimer** acepta entradas canalizadas de objetos de declinación de responsabilidades de conferencia.

## Tipos de valores devueltos

El cmdlet **Set-CsConferenceDisclaimer** no devuelve ningún objeto ni valor. En su lugar, el cmdlet modifica las instancias existentes del objeto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Vea también

#### Otros recursos

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)

