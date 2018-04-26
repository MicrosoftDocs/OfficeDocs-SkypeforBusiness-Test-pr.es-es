---
title: Test-CsDialInConferencing
TOCTitle: Test-CsDialInConferencing
ms:assetid: e4aedf4f-77ac-4c8b-9613-07f8ea12c041
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399013(v=OCS.15)
ms:contentKeyID: 48276961
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialInConferencing

 

_**Última modificación del tema:** 2015-03-09_

El cmdlet **Test-CsDialInConferencing** comprueba si un usuario puede participar en una sesión de conferencia de acceso telefónico local. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsDialInConferencing -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetPstnPhoneNumber <String>] [-UserSipAddress <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetPstnPhoneNumber <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Ejemplos

## Ejemplo 1

El ejemplo anterior verifica si el usuario de prueba preconfigurado puede participar en una conferencia de acceso telefónico local en el grupo de servidores atl-cs-001.litwareinc.com. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. Si es así, el comando averiguará si el primer usuario de prueba puede iniciar sesión en Lync Server.

Si no se han definido usuarios de prueba, el comando provocará un error porque no sabrá con qué usuario iniciar sesión. Si no se ha definido ningún usuario de prueba para un grupo de servidores, es necesario incluir el parámetro UserCredential y las credenciales del usuario que debe utilizar el comando al intentar iniciar una sesión.

    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com 

## Ejemplo 2

Los comandos del ejemplo 2 comprueban si un usuario especificado (litwareinc\\pilar) puede participar en una conferencia de acceso telefónico en el grupo de servidores atl-cs-001.litwareinc.com. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial de Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión –litwareinc\\pilar -- se ha incluido como parámetro, el administrador tiene que introducir solamente la contraseña de la cuenta de Pilar Ackerman en el cuadro de diálogo de solicitud de credenciales de Windows PowerShell.) El objeto de credencial resultante se almacena en una variable llamada $cred1.

El segundo comando comprueba si el usuario Pilar Ackerman puede iniciar una sesión en el grupo de servidores atl-cs-001.litwareinc.com y participar en una conferencia de acceso telefónico local. Para ello, se llama al cmdlet **Test-CsDialInConferencing** con tres parámetros: TargetFqdn (el nombre de dominio completo del grupo de registrador); UserCredential (el objeto de Windows PowerShell que contiene las credenciales de usuario Pilar Ackerman) y UserSipAddress (la dirección SIP correspondiente a las credenciales de usuario suministradas).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $cred1

## Descripción detallada

El cmdlet **Test-CsDialInConferencing** es un ejemplo de "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual, o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Hay dos métodos para llevar a cabo transacciones sintéticas. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar usuarios de prueba para cada grupo de registrador. Los usuarios de prueba son un par de usuarios preconfigurados para usar con transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas de usuarios reales.) Con los usuarios de prueba configurados para un grupo, los administradores pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

También es posible ejecutar una transacción sintética usando cuentas de usuario reales. Por ejemplo, si dos usuarios no pueden intercambiar mensajes instantáneos, un administrador puede ejecutar una transacción sintética usando las cuentas de dichos usuarios (en lugar de dos cuentas de prueba) e intentar diagnosticar y resolver el problema. Para llevar a cabo una transacción sintética usando cuentas de usuario reales deberá especificar los nombres de usuario y las contraseñas de cada usuario.

El cmdlet **Test-CsDialInConferencing** funciona intentando iniciar una sesión en el sistema con un usuario de prueba. (Si utiliza usuarios de prueba, el cmdlet **Test-CsDialInConferencing** usará la primera cuenta de prueba configurada en dicho grupo.) Si la sesión puede iniciarse sin problemas, el cmdlet usará las credenciales y permisos del usuario para intentar tener acceso a los números de conferencia de acceso telefónico local. Se registrará el resultado de los intentos de acceso a cada número telefónico y, a continuación, se cerrará la sesión del usuario de prueba en Lync Server.

El cmdlet **Test-CsDialInConferencing** solo verifica si pueden realizarse las conexiones correspondientes. El cmdlet no realiza ninguna llamada telefónica real ni crea ninguna conferencia de acceso telefónico local a la que puedan unirse otros usuarios.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **Test-CsDialInConferencing** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialInConferencing"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Cadena de caracteres</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo que se probará.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Objeto de credencial de la cuenta de usuario que se probará. El valor transferido a UserCredential debe ser una referencia a objeto obtenida usando el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\kenmyer y lo almacena en una variable llamada $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Debe especificar la contraseña del usuario al ejecutar este comando. Este parámetro no es obligatorio si realiza la prueba utilizando las opciones de configuración de supervisión de mantenimiento.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación utilizado en la prueba. Los valores permitidos son:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean irrecuperables y que puedan surgir al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Si está, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Esta variable incluye dos métodos, ToHTML y ToXML, que se pueden utilizar para guardar ese resultado en un archivo HTML o XML.</p>
<p>Para almacenar el resultado en una variable del registrador denominada $TestOutput, utilice la siguiente sintaxis:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: No anteponga el carácter $ al especificar el nombre de la variable. Para guardar en un archivo HTML la información almacenada en la variable del registrador, utilice un comando similar al siguiente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Para guardar en un archivo XML la información almacenada en la variable del registrador, utilice un comando similar al siguiente:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Cuando esté presente, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Por ejemplo, para almacenar resultados en una variable llamada $TestOutput, utilice la sintaxis siguiente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>No anteponga un carácter $ al especificar el nombre de variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Int32</p></td>
<td><p>Puerto SIP usado por el servicio de registrador. Este parámetro no es necesario si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Número de teléfono correspondiente a un teléfono de RTC que se usará para comprobar que los usuarios de RTC pueden unirse a la conferencia de acceso telefónico local. Por ejemplo:</p>
<p>-TargetPstnPhoneNumber &quot;+12065551219&quot;</p>
<p>Tenga en cuenta que TargetPstnPhoneNumber solo debe incluirse si usa el parámetro VerifyConferenceJoinType.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Dirección SIP de la cuenta de usuario que se probará. Por ejemplo: -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro UserSipAddress debe hacer referencia a la misma cuenta de usuario que UserCredential. Este parámetro no es obligatorio si realiza la prueba utilizando las opciones de configuración de supervisión de mantenimiento.</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyConferenceJoin</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Cuando esté establecido en True, comprueba que se pueda unir a la conferencia de acceso telefónico local mediante un teléfono de RTC. Cuando realice esta prueba, opcionalmente puede incluir TargetPstnPhoneNumber. Si lo hace, TargetPstnPhoneNumber debe especificar el teléfono de RTC que se usará para unirse a la conferencia. Si no se incluye TargetPstnPhoneNumber, el cmdlet <strong>Test-CsDialInConferencing</strong> usará los números de teléfono de acceso telefónico local preasignados a la región de la conferencia de acceso telefónico local pertinente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsDialInConferencing** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsDialInConferencing** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsAVConference](test-csavconference.md)

