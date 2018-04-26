---
title: Get-CsCommonAreaPhone
TOCTitle: Get-CsCommonAreaPhone
ms:assetid: bfb7927b-49a7-4637-a9ff-fd68897efb45
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412934(v=OCS.15)
ms:contentKeyID: 48276535
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCommonAreaPhone

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los teléfonos de área común administrados con Lync Server. Los teléfonos de área común se encuentran en salas de espera de edificios, salas de empleados u otras áreas donde puedan usarlos un número elevado de personas distintas para una amplia variedad de usos. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsCommonAreaPhone [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve información sobre todos los teléfonos de área común que actualmente están configurados para su uso en la organización. Para ello, se llama al cmdlet **Get-CsCommonAreaPhone** sin parámetros.

    Get-CsCommonAreaPhone

## Ejemplo 2

En el ejemplo 2, se devuelve el teléfono de área común con el nombre para mostrar "Building 14 Lobby" de Active Directory. Esta tarea se lleva a cabo incluyendo el parámetro -Filter y el valor de filtro {DisplayName -eq "Building 14 Lobby"}; este valor de filtro limita los objetos devueltos a los teléfonos de área común cuya propiedad DisplayName es igual a "Building 14 Lobby".

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"}

## Ejemplo 3

El comando anterior devuelve todos los teléfonos de área común que tengan un nombre para mostrar de Active Directory que comience por los caracteres "Building 14". Para ello, se llama al cmdlet **Get-CsCommonAreaPhone**, junto con el parámetro Filter y el valor de filtro {DisplayName -like "Building 14\*"}. El valor de filtro usa el operador -like y la cadena comodín "Building 14\*" para restringir los datos devueltos a los teléfonos cuya propiedad DisplayName comienza por "Building 14". Por ejemplo, "Building 14 Lobby", "Building 14 Cafeteria", etc.

    Get-CsCommonAreaPhone  -Filter {DisplayName -like "Building 14*"}

## Ejemplo 4

En el ejemplo 4, se devuelve un solo teléfono de área común: el teléfono cuya propiedad LineUri es igual a "tel:+14255551234". Dado que LineUris debe ser única, este comando no devolverá nunca más de un elemento.

    Get-CsCommonAreaPhone  -Filter {LineUri -eq "tel:+14255551234"}

## Ejemplo 5

El comando del ejemplo 5 devuelve información sobre todos los teléfonos de área común a los que no se ha asignado un plan de marcado. Para ello, se usa el parámetro Filter y el valor de filtro {DialPlan -eq $Null}, que limita los datos devueltos a los teléfonos cuya propiedad DialPlan sea igual a un valor nulo. Si no se ha asignado de forma explícita ningún plan de marcado a un teléfono de área común, el teléfono usará automáticamente el plan de marcado global o, si está disponible, el plan de marcado asignado al sitio.

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null}

## Ejemplo 6

El comando anterior devuelve una colección de todos los teléfonos de área común que tienen un objeto de contacto en la OU Telecommunications en Servicios de dominio de Active Directory. Para ello, se llama al cmdlet **Get-CsCommonAreaPhone** con el parámetro OU; el valor de parámetro limita los objetos devueltos a los teléfonos que tienen objetos de contacto en la unidad organizativa con el nombre distintivo ou=Telecommunications,dc=litwareinc,dc=com.

    Get-CsCommonAreaPhone -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## Descripción detallada

Los teléfonos de área común son teléfonos IP que no están asociados con ningún usuario concreto. En lugar de estar ubicados en una oficina, suelen encontrarse en las salas de espera de edificios, cafeterías, salas de empleados, salas de reuniones y otros lugares donde pueden confluir una gran cantidad de personas. Esto supone un reto para los administradores, ya que el uso del teléfono en Lync Server suele mantenerse con directivas de voz y planes de marcado que se asignan a usuarios concretos. Los teléfonos de área común no están asociados a ningún usuario concreto.

Una solución a este reto es crear objetos de contacto de Active Directory para todos los teléfonos de área común. (Dichos objetos de contacto se pueden crear con el cmdlet **New-CsCommonAreaPhone**). Del mismo modo que sucede con las cuentas de usuario, es posible asignar directivas y planes de marcado a los objetos de contacto. Como resultado, podrá mantener el control de los teléfonos de área común, aunque estos teléfonos no estén asociados con un usuario concreto. Por ejemplo, si no quiere que la gente tenga la posibilidad de transferir o estacionar llamadas desde un teléfono de área común, puede crear una directiva de voz que prohíba las transferencias y el estacionamiento de llamadas y, a continuación, asignarla al teléfono de área común. (O, mejor dicho, al objeto de contacto que representa el teléfono de área común). Por ejemplo, este comando asigna la directiva de voz CommonAreaPhoneVoicePolicy a todos sus teléfonos de área común:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

El cmdlet **Get-CsCommonAreaPhone** permite recuperar información sobre los teléfonos de área común configurados para su uso en la organización. Si llama al cmdlet **Get-CsCommonAreaPhone** sin ningún parámetro, el cmdlet devolverá información sobre todos sus teléfonos de área común. Los parámetros opcionales permiten filtrar información de distintas maneras; por ejemplo, puede devolver todos los teléfonos de área común que tienen objetos de contacto en una unidad organizativa (OU) especificada o todos los objetos de contactos que se encuentran en un edificio determinado.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Get-CsCommonAreaPhone** localmente: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Los permisos necesarios para ejecutar este cmdlet para sitios específicos u OU de Active Directory determinados se pueden asignar con el cmdlet **Grant-CsOUPermission**. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCommonAreaPhone"}

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
<td><p><em>Credential</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Permite iniciar el cmdlet <strong>Get-CsCommonAreaPhone</strong> con credenciales alternativas. Esto puede ser necesario si la cuenta usada para iniciar sesión en Windows no tiene los privilegios necesarios para trabajar con objetos de contacto.</p>
<p>Para usar el parámetro Credential, primero debe crear un objeto PSCredential con el cmdlet <strong>Get-Credential</strong>. Si necesita información detallada, consulte el tema de ayuda del cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Permite conectarse al controlador de dominio especificado para recuperar información de contactos. Para conectarse a un controlador de dominio específico, incluya el parámetro DomainController seguido del nombre de dominio completo (FQDN) del equipo, por ejemplo, atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite limitar los datos que se devuelven filtrando los atributos específicos de Lync Server. Por ejemplo, puede restringir los datos devueltos a objetos de contacto de teléfono de área común a los que se haya asignado una directiva de voz específica, o a contactos a los que no se haya asignado una directiva de voz específica.</p>
<p>El parámetro Filter usa la misma sintaxis de filtrado de Windows PowerShell que usa el cmdlet <strong>Where-Object</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificador único del teléfono de área común. Los teléfonos de área común se identifican con el nombre distintivo (DN) de Active Directory del objeto de contacto asociado. Los teléfonos de área común usan, de forma predeterminada, un GUID (identificador único global) como nombre común; por ello, la identidad de los teléfonos suele ser similar a la siguiente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite limitar los datos que se devuelven filtrando los atributos genéricos de Active Directory, es decir, los atributos que no son específicos de Lync Server. Por ejemplo, puede restringir los datos devueltos a los objetos de contacto que se hayan asignado a un departamento específico o que estén situados en un edificio determinado.</p>
<p>El parámetro LdapFilter usa el lenguaje de consulta LDAP al crear filtros. Por ejemplo, un filtro que devuelva solo objetos de contacto que representen teléfonos de área común de la ciudad de Redmond tendría este aspecto:</p>
<p>-LDAPFilter &quot;l=Redmond&quot;</p>
<p>En el filtro anterior, &quot;l&quot; (una L minúscula) representa el atributo de Active Directory (locality), &quot;=&quot; representa el operador de comparación (igual a) y &quot;Redmond&quot; representa el valor del filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Permite devolver objetos de contacto de una unidad organizativa (OU) de Active Directory específica. El parámetro OU devuelve datos de la unidad organizativa principal especificada y cualquier otra OU que contenga. Por ejemplo, si la OU Finance contiene dos unidades organizativas (AccountsPayable y AccountsReceivable), se devolverá la información de teléfonos de área común de las tres unidades organizativas.</p>
<p>Al especificar una OU, use el nombre distintivo del contenedor; por ejemplo: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Permite restringir el número de registros que devuelve un comando. Por ejemplo, para que se devuelvan siete teléfonos de área común (al margen de la cantidad de teléfonos de área común que haya en el bosque), incluya el parámetro -ResultSize y defina el valor en 7. Tenga en cuenta que no es posible especificar qué siete teléfonos se devolverán. Si se define el parámetro ResultSize en 7 pero solo hay tres teléfonos de área común en el bosque, el comando devolverá esos tres teléfonos y se completará sin errores.</p>
<p>El tamaño del resultado puede definirse en cualquier número entero entre 0 y 2147483647, ambos incluidos. Si se establece en 0, el comando se ejecutará pero no devolverá datos.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Cadena. El cmdlet **Get-CsCommonAreaPhone** acepta un valor de cadena canalizado que representa la identidad del teléfono de área común.

## Tipos de valores devueltos

El cmdlet **Get-CsCommonAreaPhone** devuelve instancias del objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vea también

#### Otros recursos

[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

