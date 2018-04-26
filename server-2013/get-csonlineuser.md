---
title: Get-CsOnlineUser
TOCTitle: Get-CsOnlineUser
ms:assetid: 2bfafd70-a7d9-4308-a353-5ecf44249b53
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994026(v=OCS.15)
ms:contentKeyID: 52061624
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOnlineUser

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los usuarios que tienen cuentas hospedadas en Microsoft Lync Online. Este cmdlet solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Get-CsOnlineUser [[-Identity] <UserIdParameter>] [-Filter <String>] [-LdapFilter <String>] [-OnOfficeCommunicationServer] [-OnLyncServer] [-UnAssignedUser] [-OU <OUIdParameter>] [-DomainController <Fqdn>] [-Credential <PSCredential>] [-ResultSize <Unlimited`1>] [-Verbose]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve información sobre todos los usuarios configurados como usuarios en línea.

    Get-CsOnlineUser

## Ejemplo 2

En el ejemplo 2, se devuelve información sobre un solo usuario en línea: el usuario con la dirección SIP "sip:kenmyer@litwareinc.com".

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

## Ejemplo 3

El comando del ejemplo 3 devuelve información sobre todos los usuarios en línea que se han habilitado para Lync Online pero que actualmente no están asignados a ningún grupo de registradores.

    Get-CsOnlineUser -UnassignedUser

## Ejemplo 4

El ejemplo 4 usa el parámetro Filter para limitar los datos devueltos a los usuarios en línea que tienen asignada la directiva de archivado por usuario RedmondArchiving. Para hacer esto, se usa el valor de filtro {ArchivingPolicy -eq "RedmondArchiving"}; esta sintaxis limita los datos devueltos a los usuarios donde la propiedad ArchivingPolicy es igual a (-eq) "RedmondArchiving".

    Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}

## Ejemplo 5

El ejemplo solo 5 devuelve la información correspondiente a las cuentas de usuario que se han configurado para que la cuenta no aparezca en las listas de direcciones de Microsoft Exchange. (Es decir, el atributo msExchHideFromAddressLists de Active Directory es True). Para llevar a cabo esta tarea, el parámetro Filter se incluye junto con el valor de filtro {HideFromAddressLists -eq $True}.

    Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}

## Ejemplo 6

El comando mostrado en el ejemplo 6 devuelve información sobre todos los usuarios en línea asignados al inquilino cuyo TenantID es "bf19b7db-6960-41e5-a139-2aa373474354". Para llevar a cabo esta tarea, el comando incluye el parámetro Filter junto con el valor de filtro {TenantId –eq "bf19b7db-6960-41e5-a139-2aa373474354"}. Este filtro limita los datos devueltos a los usuarios en línea asignados al inquilino "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

## Descripción detallada

El cmdlet **Get-CsOnlineUser** devuelve información sobre los usuarios que tienen cuentas hospedadas en Microsoft Lync Online. La información devuelta incluye información de cuenta estándar de Active Directory (como el departamento donde trabaja el usuario, su dirección y número de teléfono, etc.), así como información específica de Lync Server: el cmdlet **Get-CsOnlineUser** devuelve información sobre, por ejemplo, si el usuario se ha habilitado o no para la Telefonía IP empresarial y sobre qué directivas por usuario (si las hay) se han asignado al usuario.

El cmdlet **Get-CsOnlineUser** no tiene un parámetro TenantId; esto significa que no puede usar un comando como este para limitar los datos devueltos a los usuarios que tienen cuentas con un inquilino de Lync Online determinado:

    Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"

Sin embargo, si tiene varios inquilinos de Lync Online, puede devolver usuarios de un inquilino específico usando el parámetro Filter y un comando como este:

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

Este comando limita los datos devueltos a las cuentas de usuario que pertenecen al inquilino cuyo TenantId es "bf19b7db-6960-41e5-a139-2aa373474354". Si no conoce los id. del inquilino, puede devolver esa información usando este comando:

    Get-CsTenant

Si tiene una implementación híbrida o de "dominio dividido" (es decir, una implementación en la que algunos usuarios tienen cuentas hospedadas en Lync Online y otros las tienen en una versión local de Lync Server), recuerde que el cmdlet **Get-CsOnlineUser** solo devuelve información sobre los usuarios de Lync Online. Sin embargo, el cmdlet [Get-CsUser](get-csuser.md) devolverá información sobre los usuarios de Lync Online y los usuarios de Lync Server local. Si quiere excluir a los usuarios de Lync Online para que no aparezcan en los datos devueltos por el cmdlet **Get-CsUser**, use el comando siguiente:

    Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}

Por definición, los usuarios hospedados en la versión local de Lync Server siempre tendrán un TenantId igual a 00000000-0000-0000-0000-000000000000. Los usuarios hospedados en Lync Online tendrán un TenantId con un valor distinto de 00000000-0000-0000-0000-000000000000.

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
<td><p>Permite ejecutar el cmdlet <strong>Get-CsOnlineUser</strong> con credenciales alternativas. Esto puede ser necesario si la cuenta usada para iniciar sesión de Windows no tiene los privilegios necesarios para trabajar con objetos de usuario.</p>
<p>Para usar el parámetro Credential, primero debe crear un objeto PSCredential con el cmdlet <strong>Get-Credential</strong>. Si necesita información detallada, consulte el tema de ayuda del cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Permite conectarse al controlador de dominio especificado para recuperar información de usuarios. Para conectarse a un controlador de dominio específico, incluya el parámetro DomainController seguido del nombre de dominio completo (FQDN) (por ejemplo, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite limitar los datos que se devuelven filtrando los atributos específicos de Lync Server. Por ejemplo, puede limitar los datos devueltos a usuarios con una directiva de voz específica asignada o a usuarios que no tengan una directiva de voz específica asignada.</p>
<p>El parámetro Filter usa la misma sintaxis de filtrado de Windows PowerShell que usa el cmdlet Where-Object. Por ejemplo, un filtro que solo devuelve usuarios que se hayan habilitado para Telefonía IP empresarial tendría este aspecto, en el que EnterpriseVoiceEnabled representa el atributo de Active Directory, -eq representa el operador de comparación (igual a) y $True (una variable de Windows PowerShell integrada) representa el valor de filtro:</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica el parámetro Identity de la cuenta de usuario que se recuperará. Las identidades de usuario pueden especificarse con cuatro formatos: 1) la dirección SIP del usuario; 2) el nombre principal del usuario (UPN); 3) el nombre del dominio y el nombre de inicio de sesión del usuario, con formato dominio\nombre (por ejemplo, litwareinc\kenmyer), y 4) el nombre para mostrar de Active Directory del usuario (por ejemplo, Ken Myer). Además se puede hacer referencia a la cuenta del usuario al usar el nombre distintivo de Active Directory del usuario.</p>
<p>Puede usar el asterisco (*) como comodín al usar el Nombre para mostrar como identidad del usuario. Por ejemplo, el parámetro Identity &quot;* Smith&quot; devolvería todos los usuarios cuyo nombre para mostrar termine con el valor de cadena &quot; Smith&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Lo habilita para limitar los datos que se devuelven mediante el filtrado de los atributos genéricos de Active Directory, (es decir, los atributos que no son específicos de Lync Server). Por ejemplo, puede limitar los datos devueltos a usuarios que trabajan en un departamento específico o usuarios con un cargo determinado.</p>
<p>El parámetro LdapFilter usa el lenguaje de consulta LDAP al crear filtros. Por ejemplo, un filtro que devuelva solo usuarios que trabajen en la cuidad de Redmond tendría este aspecto: &quot;l=Redmond&quot;, donde &quot;l&quot; (una L minúscula) representa el atributo de Active Directory (localidad), &quot;=&quot; representa el operador de comparación (igual a) y &quot;Redmond&quot; representa el valor de filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Devuelve una recopilación de usuarios de Lync Server. Aquellos usuarios que tengan cuentas de versiones anteriores del software no serán devueltos al usar este parámetro.</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Devuelve una recopilación de usuarios de una versión anterior de Lync Server (por ejemplo, Microsoft Office Communications Server 2007 R2). Aquellos usuarios que tengan cuentas de la versión actual del software no serán devueltos al usar este parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Lo habilita para devolver información sobre las cuentas de usuario de una unidad organizativa (OU) o un contenedor específico. El parámetro OU devuelve datos de la unidad organizativa principal especificada y cualquier otra OU que contenga. Por ejemplo, si la OU Finance contiene dos unidades organizativas (AccountsPayable y AccountsReceivable), se devolverán usuarios de las tres unidades organizativas.</p>
<p>Al especificar una OU, use el nombre distintivo (DN) de ese contenedor; por ejemplo: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;. Para devolver las cuentas de usuario del contenedor de usuarios, use esta sintaxis:</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Permite limitar el número de registros que devuelve el cmdlet. Por ejemplo, para que se devuelvan siete usuarios (independientemente de la cantidad de usuarios que haya en el bosque), incluya el parámetro ResultSize y defina el valor de parámetro en 7. Tenga en cuenta que no es posible especificar qué 7 usuarios se devolverán.</p>
<p>El tamaño del resultado puede definirse en cualquier número entero entre 0 y 2147483647, ambos incluidos. Si se establece en 0, el comando se ejecutará pero no devolverá datos. Si se define el parámetro ResultSize en 7 pero solo hay tres usuarios en el bosque, el comando devolverá esos tres usuarios y se completará sin errores.</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Le permite devolver una colección de todos los usuarios que se han habilitado para Lync Online pero que no están actualmente asignados a un grupo de registradores. Los usuarios no están habilitados para iniciar sesión a menos que estén asignados a un grupo de registradores.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

El cmdlet **Get-CsOnlineUser** acepta instancias canalizadas del objeto Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser, así como valores de cadena que representan una identidad de cuenta de usuario válida (por ejemplo, "sip:kenmyer@litwareinc.com").

## Tipos de valores devueltos

El cmdlet **Get-CsOnlineUser** devuelve instancias del objeto Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser.

## Vea también

#### Otros recursos

[Get-CsUser](get-csuser.md)

