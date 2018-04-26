---
title: Set-CsExUmContact
TOCTitle: Set-CsExUmContact
ms:assetid: c0fe0fdc-6fea-4334-8645-24ffd494db07
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412944(v=OCS.15)
ms:contentKeyID: 48276547
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExUmContact

 

_**Última modificación del tema:** 2015-03-09_

Modifica un objeto de contacto de acceso de suscriptor u operador automático existente de la Mensajería unificada de Exchange (UM) hospedada. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsExUmContact -Identity <UserIdParameter> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se define la propiedad AutoAttendant del contacto Mensajería unificada de Exchange con la dirección SIP exumsa4@fabrikam.com en True. Primero se llama al cmdlet **Get-CsExUmContact** para recuperar el objeto de contacto. (También se podría haber usado el nombre para mostrar de Active Directory del contacto, el nombre principal del usuario del contacto o el nombre de inicio de sesión del contacto). Este comando recupera el contacto con el valor de Identity proporcionado. A continuación, el contacto se envía al cmdlet **Set-CsExUmContact**, donde se define el parámetro AutoAttendant en True.

    Get-CsExUmContact -Identity sip:exumsa4@fabrikam.com | Set-CsExUmContact -AutoAttendant $True

## Ejemplo 2

Este ejemplo es idéntico al ejemplo 1, pero en lugar de recuperar el contacto llamando al cmdlet **Get-CsExUmContact** y canalizando el objeto al cmdlet **Set-CsExUmContact**, se proporciona a **Set-CsExUmContact** el valor de Identity del contacto que se quiere modificar. Preste atención al formato del parámetro Identity: en este caso, hemos usado el nombre distintivo completo del objeto de contacto, que incluye un GUID generado automáticamente (generado al crear el contacto). A continuación, se define el parámetro AutoAttendant del contacto en True.

    Set-CsExUmContact -Identity "CN={1bf6208d-2847-45d0-828f-636f14da858b},OU=ExUmContacts,DC=litwareinc,DC=com" -AutoAttendant $True

## Descripción detallada

Lync Server funciona en combinación con Mensajería unificada de Exchange para ofrecer varias capacidades de voz, como operador automático y acceso de suscriptor. Cuando Mensajería unificada de Exchange se ofrece como un servicio hospedado (no instalado en la organización), deben crearse objetos de contacto con Windows PowerShell para aplicar las funciones de operador automático y acceso de suscriptor. Estos objetos se crean llamando al cmdlet **New-CsExUmContact** y pueden modificarse posteriormente con el cmdlet **Set-CsExUmContact**.

La forma más fácil de usar este cmdlet es, en primer lugar, llamar al cmdlet **Get-CsExUmContact** para recuperar una instancia del objeto de contacto que quiere modificar. Canalizar el resultado del comando **Get-CsExUmContact** al cmdlet **Set-CsExUmContact** y asignar valores a los parámetros para las propiedades que quiera cambiar. (Para obtener más información, vea la sección de ejemplos de este tema). También puede llamar al cmdlet **Set-CsExUmContact**, enviándole el valor de Identity del objeto de contacto que quiera modificar.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsExUmContact** localmente: RTCUniversalUserAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExUmContact"}

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
<td><p>Identificador único del objeto de contacto que se quiere modificar. Las identidades de contacto pueden especificarse con cuatro formatos: 1) La dirección SIP del contacto; 2) el nombre principal (UPN) del usuario del contacto; 3) el nombre de dominio y nombre de inicio de sesión del contacto con formato dominio\nombre (por ejemplo, litwareinc\exum1); y, 4) el nombre para mostrar de Active Directory del contacto (por ejemplo, Team Auto Attendant).</p>
<p>Tipo de datos completo: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendant</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Defina el parámetro en True, si el objeto de contacto es un operador automático. Este parámetro es False de forma predeterminada.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Descripción de este contacto. La descripción permite a los administradores identificar el tipo de contacto (operador automático o acceso de suscriptor), la ubicación, el proveedor o cualquier otra información que identifique el propósito de cada contacto de Mensajería unificada de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>El número de teléfono del contacto. Los números para mostrar de cada contacto deben ser únicos (no puede haber dos contactos de Mensajería unificada de Exchange con el mismo número para mostrar). Si se cambia este valor, se cambiará también el valor de la propiedad LineURI.</p>
<p>Este valor puede empezar con un signo más (+) y puede contener cualquier cantidad de dígitos. El primer dígito no puede ser cero.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Fqdn</p></td>
<td><p>Permite especificar un controlador de dominio. Si no se especifica ninguno, se usará el primero que haya disponible.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si el contacto se ha habilitado para Lync Server. Si define este parámetro en False, se deshabilitará el contacto y el operador automático o el acceso de suscriptor asociado con el contacto no funcionará.</p>
<p>Si se deshabilita una cuenta con el parámetro Enabled, se conserva la información asociada con la cuenta (incluidas las directivas de correo de voz hospedado asignadas). Si se reactiva la cuenta más adelante con el parámetro Enabled, la información asociada con la cuenta se restaurará.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si el contacto se ha habilitado para telefonía IP empresarial. Si define este valor en False, no estará disponible la característica de operador automático o acceso de suscriptor asociada con el contacto.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica dónde se archivan las sesiones de mensajería instantánea del contacto. Los valores permitidos son:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Opcional</p></td>
<td><p>witchParameter</p></td>
<td><p>Devuelve los resultados del comando. De forma predeterminada, este cmdlet no genera resultados.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La dirección SIP del contacto. Debe ser una dirección nueva que no exista ya como usuario o contacto en Servicios de dominio de Active Directory.</p>
<p>Si se cambia este valor, también cambiará la dirección SIP almacenada en la propiedad OtherIpPhone.</p>
<p>El parámetro SipAddress se puede usar como valor de Identity con los comandos cmdlet <strong>Get-CsExUmContact</strong> para recuperar contactos específicos. Al llamar al cmdlet, se usará el nuevo parámetro SipAddress; las consultas de la dirección SIP antigua no devolverán ningún objeto.</p></td>
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

Objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Acepta la entrada canalizada de objetos de contacto de Mensajería unificada de Exchange.

## Tipos de valores devueltos

Este cmdlet modifica un objeto de tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Cuando se usa el parámetro PassThru, también devuelve un objeto de este tipo.

## Vea también

#### Otros recursos

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

