---
title: Test-CsAddressBookWebQuery
TOCTitle: Test-CsAddressBookWebQuery
ms:assetid: 9753dcba-83b3-437b-98f0-2806305a5bbb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398773(v=OCS.15)
ms:contentKeyID: 48276102
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookWebQuery

 

_**Última modificación del tema:** 2015-03-09_

Prueba la capacidad de un usuario para buscar y devolver información de la libreta de direcciones con el Servicio de consulta web de libreta de direcciones. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsAddressBookWebQuery -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TargetSipAddress <String>]

## Ejemplos

## Ejemplo 1

En el ejemplo anterior se prueba el Servicio de consulta web de libreta de direcciones con el grupo atl-cs-001.litwareinc.com; para ello, se busca al contacto con la dirección SIP sip:kenmyer@litwareinc.com. Este comando solo funcionará si se han definido usuarios de prueba para el grupo atl-cs-001.litwareinc.com. Si se ha definido, el comando se ejecutará con las credenciales del primer usuario de pruebas definido para este grupo.

Si no se han definido los usuarios de prueba, el comando no se ejecutará correctamente. Si no se han definido usuarios de prueba para un grupo, debe incluir el parámetro UserSipAddress y las credenciales del usuario con el que debe ejecutarse el comando.

    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com  -TargetSipAddress "sip:kenmyer@litwareinc.com"

## Ejemplo 2

Los comandos del ejemplo 2 también sirven para probar la disponibilidad de Servicio de consulta web de libreta de direcciones; sin embargo, en este caso, los comandos se ejecutan con las credenciales del usuario Ken Myer (litwareinc\\kenmyer). Para hacerlo, el primer comando usa el cmdlet **Get-Credential** para crear un objeto de credenciales Windows PowerShell que contiene el nombre y la contraseña del usuario Ken Myer. (Dado que el nombre de inicio de sesión, litwareinc\\kenmyer, se ha incluido como parámetro, el cuadro de diálogo de petición de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Ken Myer). El objeto de credenciales resultante se almacena a continuación en una variable llamada $cred1.

En el segundo comando, se usa el cmdlet **Test-CsAddressBookWebQuery** para probar el Servicio de consulta web de libreta de direcciones en el grupo atl-cs-001.litwareinc.com. Para ejecutar este comando con las credenciales de usuario de Ken Myer, se incluye el parámetro UserCredential con el valor de parámetro $cred1. El comando usa también TargetSipAddress para especificar que el cmdlet debe buscar en la libreta de direcciones el contacto con la dirección SIP sip:kenmyer@litwareinc.com.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## Ejemplo 3

En el ejemplo 3, se muestra cómo probar el Servicio de consulta web de libreta de direcciones para atl-cs-001.litwareinc.com. Para ello, se llama al cmdlet **Test-CsAddressBookWebQuery** con tres parámetros: TargetUri, que especifica el URI del Servicio de consulta web de libreta de direcciones; UserSipAddress, que contiene la dirección SIP de Windows PowerShell correspondiente a la cuenta de usuario que se está probando; y TargetSipAddress, que contiene la dirección SIP de la cuenta de usuario que se está buscando.

    Test-CsAddressBookWebQuery -TargetUri https://atl-cs-001.litwareinc.com/groupexpansion -UserSipAddress "sip:packerman@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## Descripción detallada

El cmdlet **Test-CsAddressBookWebQuery** es un ejemplo de "transacción sintética". Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios puedan completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o hacer llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede iniciarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Hay dos métodos para llevar a cabo transacciones sintéticas. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar usuarios de prueba para cada grupo de registradores. Estos usuarios de prueba son un par de usuarios preconfigurados para usar transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas de usuarios reales). Con los usuarios de prueba configurados para un grupo de servidores, los administradores pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

También es posible iniciar una transacción sintética con cuentas de usuario reales. Por ejemplo, si dos usuarios no pueden intercambiar mensajes instantáneos, un administrador puede ejecutar una transacción sintética con esas dos cuentas de usuario (en lugar de dos cuentas de prueba) e intentar diagnosticar y resolver el problema. Para llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar los nombres de usuario y las contraseñas de cada usuario.

El cmdlet **Test-CsAddressBookWebQuery** permite a los administradores comprobar que los usuarios puedan usar el Servicio de consulta web de libreta de direcciones para buscar un determinado contacto. Al ejecutar el cmdlet, **Test-CsAddressBookWebQuery** se conectará primero al servicio de vales web para autenticarse. Si la autenticación se realiza correctamente, el cmdlet se conectará entonces al Servicio de consulta web de libreta de direcciones y buscará el contacto. Si lo encuentra, el cmdlet intentará devolver la información al equipo local. La prueba solo se considerará superada si se completan todos estos pasos.

Quién puede iniciar este cmdlet: para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookWebQuery"}

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
<td><p>Cadena</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo de registradores en el que se probará la Servicio de consulta web de libreta de direcciones. Por ejemplo: -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Tenga en cuenta que no se pueden usar ambos parámetros, TargetUri y TargetFqdn, dentro del mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Cadena</p></td>
<td><p>Identificador de recursos uniforme (URI) de Servicio de consulta web de libreta de direcciones. Por ejemplo: -TargetUri &quot;https://atl-cs-001.litwareinc.com/groupexpansion&quot;.</p>
<p>Tenga en cuenta que no se pueden usar ambos parámetros, TargetUri y TargetFqdn, dentro del mismo comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credencial de usuario de la cuenta de usuario que se usará en la prueba. El valor transferido a -UserCredential debe ser una referencia a objeto obtenida con el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\kenmyer y almacena dicho objeto en una variable llamada</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Debe facilitar la contraseña de usuario al iniciar este comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación usada en la prueba. Los valores permitidos son:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Permite verificar si los usuarios externos pueden usar la Servicio de consulta web de libreta de direcciones.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Si está presente, el resultado detallado de iniciar el cmdlet se almacenará en la variable especificada. Esta variable incluye un par de métodos (ToHTML y ToXML) que se pueden usar para guardar el resultado en un archivo HTML o XML.</p>
<p>Para almacenar el resultado en una variable de registrador llamada $TestOutput, use la sintaxis siguiente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: no anteponga un carácter $ al especificar el nombre de variable. Para guardar en un archivo HTML la información almacenada en la variable de registrador, use un comando similar a este:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Para guardar en un archivo XML la información almacenada en la variable de registrador, use un comando similar a este:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Si está presente, el resultado detallado de iniciar el cmdlet se almacenará en la variable especificada. Por ejemplo, para almacenar resultados en una variable llamada $TestOutput, use la sintaxis siguiente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>No anteponga un carácter $ al especificar el nombre de variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Puerto SIP usado por el servicio de registrador. Este parámetro no es necesario si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección SIP del contacto que se espera que devuelva el Servicio de consulta web de libreta de direcciones. Por ejemplo: -TargetSipAddress &quot;sip:kenmyer@litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección SIP del usuario que se usará en la prueba. Si este parámetro no está especificado, el cmdlet <strong>Test-CsAddressBookWebQuery</strong> realizará comprobaciones con las opciones de configuración de seguimiento de estado para el grupo que se está probando.</p></td>
</tr>
<tr class="even">
<td><p><em>WebCredential</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto que contiene credenciales de usuario para obtener acceso al servicio de información de ubicaciones. Este objeto se puede recuperar llamando al cmdlet <strong>Get-Credential</strong> y facilitando las credenciales correspondientes.</p>
<p>Este parámetro es necesario si se han especificado los parámetros TargetUri y UserSipAddress y si el PC en el que el comando se inicia carece de un certificado de servidor.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsAddressBookWebQuery** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsAddressBookWebQuery** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Update-CsAddressBook](update-csaddressbook.md)

