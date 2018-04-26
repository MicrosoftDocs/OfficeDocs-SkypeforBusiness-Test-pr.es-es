---
title: Set-CsCommonAreaPhone
TOCTitle: Set-CsCommonAreaPhone
ms:assetid: 765ab74c-33ca-4b17-ba15-edb2fe559ebb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398579(v=OCS.15)
ms:contentKeyID: 48275699
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCommonAreaPhone

 

_**Última modificación del tema:** 2015-03-09_

Modifica los valores de propiedades de un teléfono de área común administrado por Lync Server. Los teléfonos de área común están ubicados en las salas de espera de edificios, salas de empleados u otras áreas donde una gran cantidad de personas puede empelarlos para usos diversos. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En el ejemplo 1, se modifica el nombre para mostrar de Active Directory para el teléfono de área común con el número 1-425-555-6710. Para ello, primero se llama al cmdlet **Get-CsCommonAreaPhone** con el parámetro Filter; el valor de filtro {LineUri -eq "tel:+14255556710"} limita los datos devueltos al teléfono de área común cuya propiedad LineUri sea igual a tel:+14255556710. Después, el objeto devuelto se canaliza al cmdlet **Set-CsCommonAreaPhone**, que establece el valor de la propiedad DisplayName en "Employee Lounge".

    Get-CsCommonAreaPhone -Filter {LineUri -eq "tel:+14255556710"} | Set-CsCommonAreaPhone -DisplayName "Employee Lounge"

## Ejemplo 2

El comando del ejemplo 2 habilita todos los teléfonos de área común actualmente configurados para uso en la organización. Para hacer esta tarea, el comando llama al cmdlet **Get-CsCommonAreaPhone** sin ningún parámetro para que devuelva una colección de todos los teléfonos de área común. Después, esta colección se canaliza al cmdlet **Set-CsCommonAreaPhone**, que establece el valor de la propiedad Enabled en True para todos los elementos de la colección.

    Get-CsCommonAreaPhone | Set-CsCommonAreaPhone -Enabled $True

## Ejemplo 3

En el ejemplo 3, se agrega una descripción genérica a todos los teléfonos de área común que no tienen asignado ningún valor en la propiedad Description. Para ello, se llama al cmdlet **Get-CsCommonAreaPhone** con el parámetro Filter; el valor de filtro {Description -eq $Null} garantiza que los únicos elementos devueltos sean teléfonos de área común cuya propiedad Description sea igual a un valor nulo. Después, la colección filtrada se canaliza al cmdlet **Set-CsCommonAreaPhone**, que asigna la descripción genérica "Common area phone" a todos los elementos de la colección.

    Get-CsCommonAreaPhone -Filter {Description -eq $Null} | Set-CsCommonAreaPhone -Description "Common area phone"

## Descripción detallada

Los teléfonos de área común son teléfonos IP que no están asociados a un usuario individual. En lugar de estar ubicados en la oficina de algún empleado, los teléfonos de área común suelen estar en salas de espera de edificios, cafeterías, salas de empleados, salas de reuniones y otros lugares donde pueden confluir una gran cantidad de personas. Esto supone un reto de administración para los administradores, ya que el uso del teléfono en Lync Server suele mantenerse con directivas de voz y planes de marcado que se asignan a usuarios individuales. Los teléfonos de área común no tienen usuarios individuales asignados.

Una solución a este reto es crear objetos de contacto de Active Directory para todos los teléfonos de área común (se pueden crear con el cmdlet **New-CsCommonAreaPhone**). Igual que sucede con las cuentas de usuario, es posible asignar directivas y planes de marcado a los objetos de contacto. Como resultado, podrá mantener el control de los teléfonos de área común aunque no estén asociados a un usuario concreto. Por ejemplo, si no quiere que se puedan transferir o estacionar llamadas desde un teléfono de área común, cree una directiva de voz que prohíba las transferencias y el estacionamiento de llamadas y asígnela al teléfono de área común. (O, mejor dicho, al objeto de contacto que representa el teléfono de área común). Este comando asigna la directiva de voz CommonAreaPhoneVoicePolicy a todos los teléfonos de área común:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

El cmdlet **Set-CsCommonAreaPhone** permite modificar las propiedades de los objetos de contacto asociados con los teléfonos de área común. Entre otras cosas, puede cambiar el nombre para mostrar de Active Directory del contacto o el URI de línea asociado con el teléfono. También puede usar el parámetro Enabled para habilitar y deshabilitar el uso de la cuenta con Lync Server.

Además, puede configurar "áreas de trabajo sin asignar" para los teléfonos de área común con los cmdlet CsClientPolicy. Cuando se indica un teléfono para un área de trabajo no asignada, los usuarios pueden iniciar sesión en el teléfono con sus credenciales Lync Server. Entre otras cosas, esto les ofrece un acceso fácil a sus contactos. Consulte el tema de ayuda del cmdlet [Set-CsClientPolicy](set-csclientpolicy.md) para obtener más información.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para iniciar el cmdlet **Set-CsCommonAreaPhone** localmente: RTCUniversalUserAdmins. Se pueden asignar permisos para ejecutar este cmdlet para sitios específicos o unidades organizativas (OU) de Active Directory por medio del uso del cmdlet **Grant-CsOUPermission**. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCommonAreaPhone"}

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
<td><p>UserIdParameter</p></td>
<td><p>Identificador único del teléfono de área común. Los teléfonos de área común se identifican con el nombre distintivo de Active Directory del objeto de contacto asociado. De forma predeterminada, los teléfonos de área común usan un GUID (identificador único global) como nombre común; esto significa que los teléfonos normalmente tienen una identidad similar a esta: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Por este motivo, es posible que le resulte más fácil recuperar los teléfonos de área común si usa el cmdlet <strong>Get-CsCommonAreaPhone</strong> y luego canaliza los objetos devueltos al cmdlet <strong>Set-CsCommonAreaPhone</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Permite modificar el atributo de descripción de Active Directory para el teléfono de área común. Esto permite proporcionar información adicional sobre el teléfono como por ejemplo, detalles sobre con quién debe ponerse en contacto si surgen problemas con el teléfono.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Permite modificar el nombre para mostrar de Active Directory del teléfono de área común.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Número de teléfono tal como aparece en Lync. Puede asignar el formato que prefiera a la propiedad DisplayNumber; por ejemplo, 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234, etc. Al elegir un número para mostrar, tenga en cuenta que este número aparecerá en la pantalla del teléfono de área común solo si se puede normalizar el número. (Normalización es el proceso de traducción de cadenas de números en un formato de número telefónico estándar). Si no existe una regla de normalización para el formato de número telefónico usado al configurar el número para mostrar, la pantalla del teléfono de área común mostrará el valor de la propiedad LineUri en lugar del valor de la propiedad DisplayNumber.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Fqdn</p></td>
<td><p>Permite conectarse al controlador de dominio especificado para modificar la información de contacto. Para conectarse a un controlador de dominio específico, debe incluir el parámetro DomainController seguido del nombre del equipo (por ejemplo, atl-mcs-001) o su nombre de dominio completo (FQDN), por ejemplo: atl-mcs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si el objeto de contacto del teléfono de área común se ha habilitado para Lync Server.</p>
<p>Si se deshabilita un contacto con el parámetro Enabled, la información asociada con esa cuenta se conservará (incluidas las directivas asignadas, si el usuario está habilitado para telefonía IP empresarial, el control remoto de llamadas y la integración de correo de voz). Si se vuelve a habilitar la cuenta más adelante con el parámetro Enabled, la información asociada con la cuenta se restaurará.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si el objeto de contacto del teléfono de área común se ha habilitado para telefonía IP empresarial, la solución de Microsoft que usa el protocolo de voz sobre IP (VoIP). Con la telefonía IP empresarial, las llamadas telefónicas se pueden hacer a través de Internet en lugar de usar la red telefónica estándar.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica si se archivan las sesiones de mensajería instantánea del contacto. Los valores permitidos son:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Número de teléfono del teléfono de área común. El identificador uniforme de recursos (URI) de línea debe especificarse en el formato E.164 y con el prefijo &quot;TEL:&quot;. Por ejemplo: TEL:+14255551297. Los números de extensión deben agregarse al final del URI de línea, por ejemplo: TEL:+14255551297; ext=51297.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Devuelve un objeto que representa el teléfono de área común.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Identificador único que permite que el teléfono de área común se comunique con dispositivos SIP, como Lync. La dirección SIP debe tener el prefijo sip: e incluye un dominio SIP válido. Por ejemplo: sip:bldg14lobby@litwareinc.com.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Tipos de valores devueltos

De manera predeterminada, el cmdlet **Set-CsCommonAreaPhone** no devuelve ningún valor ni objeto. No obstante, si incluye el parámetro PassThru, el cmdlet devolverá instancias del objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vea también

#### Otros recursos

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)

