---
title: Move-CsCommonAreaPhone
TOCTitle: Move-CsCommonAreaPhone
ms:assetid: af5f832c-1be9-4495-ba1a-c10ca50d7b29
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412837(v=OCS.15)
ms:contentKeyID: 48276355
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsCommonAreaPhone

 

_**Última modificación del tema:** 2015-04-02_

Mueve uno o más teléfonos de área común a un nuevo grupo de registradores. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Move-CsCommonAreaPhone -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 modifica el teléfono de área común con la identidad CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com para el grupo de registradores atl-cs-001.litwareinc.com.

    Move-CsCommonAreaPhone -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## Ejemplo 2

En el ejemplo 2, se mueve el teléfono de área común con el nombre para mostrar de Active Directory "Building 31 Cafeteria" al grupo de registradores atl-cs-001.litwareinc.com. Para ello, primero se llama al cmdlet **Get-CsCommonAreaPhone** sin ningún parámetro para devolver una colección de todos los teléfonos de área común que están en uso en la organización. Después, la colección se canaliza al cmdlet **Where-Object**, que elige solo los teléfonos en los que el atributo DisplayName es igual a "Building 31 Cafeteria". Luego, la colección filtrada se canaliza al cmdlet **Move-CsCommonAreaPhone**, que mueve cada teléfono de la colección a atl-cs-001.litwareinc.com.

    Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -eq "Building 31 Cafeteria"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## Ejemplo 3

En el ejemplo 3, se muestra cómo se mueven todos los teléfonos de área común que actualmente se encuentran en el grupo de registradores dublin-cs-001.litwareinc.com al grupo de registradores atl-cs-001.litwareinc.com. Para llevar a cabo esta tarea, el comando llama primero al cmdlet **Get-CsCommonAreaPhone** sin ningún parámetro, que devuelve una colección de todos los teléfonos de área común configurados para usarse en la organización. Después, la colección se canaliza al cmdlet **Where-Object**, que elige todos los teléfonos de área común en los que la propiedad RegistrarPool es igual a dublin-cs-001.litwareinc.com. Luego, la colección se canaliza al cmdlet **Move-CsCommonAreaPhone**, que mueve cada teléfono de la colección al nuevo grupo de registradores atl-cs-001.litwareinc.com.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## Ejemplo 4

El ejemplo 4 es una variación del comando que se muestra en el ejemplo 3, pero en este caso, los teléfonos de área común no solo se mueven a un nuevo grupo de registradores, sino que también se les asigna una nueva directiva de voz por usuario. Para hacerlo, el parámetro PassThru se incluye al llamar al cmdlet **Move-CsCommonAreaPhone**; esto es necesario a fin de pasar los objetos de los teléfonos de área común a través de la canalización. (De manera predeterminada, el cmdlet **Move-CsCommonAreaPhone** no pasa objetos por canalización). Después de mover los teléfonos, los objetos del teléfono se canalizan al cmdlet **Grant-CsVoicePolicy**, que asigna la directiva de voz AtlantaVoicePolicy a cada uno de los teléfonos que se acaban de mover.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com -PassThru | Grant-CsVoicePolicy -PolicyName AtlantaVoicePolicy

## Descripción detallada

Los teléfonos de área común son teléfonos IP que no están asociados a un usuario individual. En lugar de estar ubicados en la oficina de algún empleado, los teléfonos de área común suelen encontrarse en salas de espera de edificios, cafeterías, salas de empleados, salas de reuniones y otros lugares donde pueden confluir una gran cantidad de personas. Esto supone un reto de administración para los administradores; esto se debe a que el uso del teléfono en Lync Server suele mantenerse con directivas de voz y planes de marcado que se asignan a usuarios individuales. Los teléfonos de área común no tienen usuarios individuales asignados.

La solución a este reto es crear objetos de contacto de Active Directory para todos los teléfonos de área común. (Dichos objetos de contacto se pueden crear con el cmdlet **New-CsCommonAreaPhone**). Del mismo modo que sucede con las cuentas de usuario, es posible asignar directivas y planes de marcado a los objetos de contacto. Como resultado, podrá mantener el control de los teléfonos de área común, aunque estos teléfonos no estén asociados con un usuario concreto. Por ejemplo, si no quiere que la gente tenga la posibilidad de transferir o estacionar llamadas desde un teléfono de área común, puede crear una directiva de voz que prohíba las transferencias y el estacionamiento de llamadas y, a continuación, asignarla al teléfono de área común. (O, mejor dicho, al objeto de contacto que representa el teléfono de área común).

El cmdlet **Move-CsCommonAreaPhone** permite mover un teléfono de área común a un grupo de registradores nuevo.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para iniciar el cmdlet **Move-CsCommonAreaPhone** localmente: RTCUniversalUserAdmins. Se pueden asignar permisos para ejecutar este cmdlet para sitios específicos o unidades organizativas (OU) de Active Directory por medio del uso del cmdlet **Grant-CsOUPermission**. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsCommonAreaPhone"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificador único del teléfono de área común. Los teléfonos de área común se identifican con el nombre distintivo de Active Directory del objeto de contacto asociado. De forma predeterminada, los teléfonos de área común, usan un GUID (identificador único global) como nombre común; esto significa que los teléfonos normalmente tienen una identidad similar a esta: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>El nombre de dominio completo (FQDN) del grupo de registradores al que se debe mover el teléfono de área común; por ejemplo: atl-cs-001.litwareinc.com. Además del grupo de registradores, el objetivo también puede ser el FQDN de un proveedor de hospedaje.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Permite conectarse al controlador de dominio especificado para mover el teléfono de área común. Para conectarse a un controlador de dominio específico, debe incluir el parámetro DomainController seguido del nombre del equipo (por ejemplo, atl-cs-001) o su FQDN (por ejemplo, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Si se especifica, mueve el teléfono de área común pero elimina los datos asociados, como directivas asignadas al dispositivo). Si no se especifica, el teléfono se mueve junto con los datos asociados.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Si está presente, indica al PC que ignore los errores que se puedan producir con la base de datos back-end y que intente mover el teléfono de área común igualmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Permite enviar un objeto de usuario a través de la canalización que representa la cuenta de usuario que se está moviendo. De manera predeterminada, el cmdlet <strong>Move-CsCommonAreaPhone</strong> no pasa objetos por la canalización.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Este parámetro se usa solo para Lync Online. No debe usarse en una instalación interna de Lync Server.</p></td>
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

Cadena. El cmdlet **Move-CsCommonAreaPhone** acepta un valor de cadena canalizado que representa la identidad del teléfono de área común.

## Tipos de valores devueltos

De forma predeterminada, el cmdlet **Move-CsCommonAreaPhone** no devuelve ningún valor ni objeto. Sin embargo, si incluye el parámetro PassThru, el cmdlet devolverá instancias del objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vea también

#### Otros recursos

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

