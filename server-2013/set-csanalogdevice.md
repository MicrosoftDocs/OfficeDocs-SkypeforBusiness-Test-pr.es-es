---
title: Set-CsAnalogDevice
TOCTitle: Set-CsAnalogDevice
ms:assetid: b05e729e-cdef-4c78-8ce7-b183c3208a93
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412843(v=OCS.15)
ms:contentKeyID: 48276373
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnalogDevice

 

_**Última modificación del tema:** 2015-03-09_

Modifica un dispositivo existente de la colección de dispositivos analógicos que se pueden administrar con Lync Server. Un dispositivo analógico es un teléfono o dispositivo de fax conectado a la red telefónica conmutada (RTC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsAnalogDevice -Identity <UserIdParameter> [-AnalogFax <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-Gateway <Fqdn>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando anterior cambia el valor de la propiedad LineUri del dispositivo analógico que tiene la identidad CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.

    Set-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -LineUri "TEL:+14255551298"

## Ejemplo 2

El comando que aparece en el ejemplo 2 modifica la puerta de enlace de cada dispositivo analógico que está usando la puerta de enlace 192.168.0.240. Para realizar esta tarea, se llama al cmdlet **Get-CsAnalogDevice** junto con el parámetro Filter; el valor de filtro {Gateway -eq "192.168.0.240"} garantiza que se devuelvan solo los dispositivos cuyo valor Gateway sea igual a (-eq) 192.168.0.240. Después la colección filtrada se canaliza al cmdlet **Set-CsAnalogDevice**, que toma cada elemento de la colección y modifica el valor de la propiedad Gateway a 192.168.1.100.

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"} | Set-CsAnalogDevice -Gateway "192.168.1.100"

## Descripción detallada

Los dispositivos analógicos pueden ser teléfonos, aparatos de fax, módems y dispositivos TTY/TTD (Teletype/Telecommunication Devices for the Deaf) conectados a la red telefónica conmutada (RTC). A diferencia de los dispositivos que usan telefonía IP empresarial (es decir, el sistema de Microsoft para el protocolo de voz sobre IP (VoIP)), los dispositivos analógicos no transmiten la información con paquetes digitales. En su lugar, la información se transmite a través de señales continuas. Esta señal se denomina señal analógica; de ahí el término “dispositivos analógicos”.

Para que los administradores puedan controlar dispositivos analógicos, Lync Server permite asociarlos con objetos de contacto de Active Directory. Al asociar un dispositivo analógico con un objeto de contacto, puede administrarlo asignando directivas y planes de marcado al contacto.

El cmdlet **Set-CsAnalogDevice** proporciona una forma de modificar las propiedades de los objetos de contacto asociados con dispositivos analógicos. Por ejemplo, es posible cambiar el nombre para mostrar de Active Directory del contacto o el Identificador uniforme de recursos (URI) asociado con el dispositivo.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **Set-CsAnalogDevice** localmente: RTCUniversalUserAdmins. Los permisos para ejecutar este cmdlet para sitios específicos o unidades organizacionales (OU) específicas de Active Directory pueden asignarse por medio del cmdlet **Grant-CsOUPermission**. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles RBAC personalizados que haya creado usted mismo), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnalogDevice"}

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
<td><p>Identificador único para el dispositivo analógico objeto de modificación. Los dispositivos analógicos se identifican con el nombre distintivo (DN) de Active Directory correspondiente al objeto del contacto asociado. De forma predeterminada, los dispositivos analógicos usan un GUID (identificador único global) como nombre común; por ello, la identidad de los dispositivos suele ser similar a la siguiente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Debido a esto, es posible que resulte más fácil modificar los dispositivos analógicos con el cmdlet <strong>Get-CsAnalogDevice</strong> para devolver los objetos de los dispositivos analógicos y después canalizar esos objetos al cmdlet <strong>Set-CsAnalogDevice</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AnalogFax</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Se establece en True ($True) si el dispositivo analógico es un fax. Se establece en False ($False) si el dispositivo no es una máquina de fax.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Configura el nombre para mostrar de Active Directory del dispositivo analógico.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>El número de teléfono tal y como aparece en Lync. Puede dar el formato que prefiera a la propiedad DisplayNumber; por ejemplo, 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234, etc.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Fqdn</p></td>
<td><p>Permite conectarse al controlador de dominio especificado para modificar la información de contacto. Para conectarse a un controlador de dominio específico, debe incluir el parámetro DomainController seguido del nombre del equipo (por ejemplo, atl-mcs-001) o su nombre de dominio completo (FQDN) (por ejemplo, atl-mcs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Si está definido en True ($True), el dispositivo analógico puede usarse con Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si el objeto de contacto del dispositivo analógico está habilitado para telefonía IP empresarial, la solución de VoIP de Microsoft. Con la telefonía IP empresarial, las llamadas telefónicas se pueden realizar a través de Internet, en lugar de usar la red telefónica estándar.</p></td>
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
<td><p><em>Gateway</em></p></td>
<td><p>Opcional</p></td>
<td><p>Fqdn</p></td>
<td><p>Dirección IP de la puerta de enlace RTC que usará el dispositivo analógico.</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Número de teléfono del dispositivo analógico. El URI de línea debe especificarse en el formato E.164 y con el prefijo &quot;TEL:&quot;. Por ejemplo: TEL:+14255551297. Los números de extensión deben agregarse al final del URI de línea, por ejemplo: TEL:+14255551297; ext=51297.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Opcional</p></td>
<td><p>witchParameter</p></td>
<td><p>Devuelve un objeto que representa el teléfono de área común.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Identificador único que permite al dispositivo analógico comunicarse con dispositivos SIP, como por ejemplo Lync 2013. La dirección SIP debe tener el prefijo &quot;sip:&quot;. Por ejemplo: sip:bldg14lobby@litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact. El cmdlet **Set-CsAnalogDevice** acepta las instancias canalizadas del objeto del dispositivo analógico.

## Tipos de valores devueltos

De forma predeterminada, el **Set-CsAnalogDevice** no devuelve ningún valor u objeto. Sin embargo, si incluye el parámetro PassThru, el cmdlet devolverá instancias del objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Vea también

#### Otros recursos

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)

