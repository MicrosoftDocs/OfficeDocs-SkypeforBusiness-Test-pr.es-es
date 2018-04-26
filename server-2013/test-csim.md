---
title: Test-CsIM
TOCTitle: Test-CsIM
ms:assetid: 2fdab54c-5ec4-4db5-b29c-a3efaae68f66
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425802(v=OCS.15)
ms:contentKeyID: 48274832
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsIM

 

_**Última modificación del tema:** 2015-03-09_

Prueba la capacidad de dos usuarios para intercambiar mensajes instantáneos. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-EmailHost <String>] [-Force <SwitchParameter>] [-IsSsl <$true | $false>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Password <String>] [-Port <UInt16>] [-TestLegalIntercept <SwitchParameter>] [-Username <String>] [-WaitSeconds <Int16>]

## Ejemplos

## EJEMPLO 1

El ejemplo 1 comprueba si un par de usuarios de prueba preconfigurados pueden iniciar sesión en el grupo atl-cs-001.litwareinc.com y, luego, intercambiar mensajes instantáneos. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. Si se ha definido, el comando determinará si los dos usuarios pueden iniciar sesión en el sistema y, de ser así, pueden intercambiar mensajes instantáneos. Si

Si no se han definido usuarios de prueba, se producirá un error en el comando porque no sabrá qué usuario emplear para realizar la prueba. Si no se ha definido un registrador para un grupo, deberá incluir los parámetros SenderSipAddress y ReceiverSipAddress, además de las credenciales correspondientes de los usuarios implicados en la sesión de mensajería instantánea. A continuación, el cmdlet **Test-CsIM** realizará sus comprobaciones con los dos usuarios especificados.

    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com

## EJEMPLO 2

Los comandos que se muestran en el ejemplo 2 prueban la capacidad de un par de usuarios (litwareinc\\pilar y litwareinc\\kenmyer) de iniciar sesión en Lync Server, y después intercambiar mensajes instantáneos. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de solicitud de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). Luego, el objeto de credenciales resultante se almacena en una variable denominada $cred1. El segundo comando hace lo mismo, pero devuelve un objeto de credenciales para la cuenta de Ken Myer.

Con ambos objetos credencial en mano, el tercer comando del ejemplo determina si los dos usuarios pueden o no iniciar sesión en Lync Server e intercambiar mensajes instantáneos. Para ello, se llama al cmdlet **Test-CsIM** junto con los siguientes parámetros: TargetFqdn (el FQDN del grupo de registradores), SenderSipAddress (la dirección SIP del primer usuario de prueba), SubscriberCredential (el objeto de Windows PowerShell que contiene las credenciales de este usuario), -ReceiverSipAddress (la dirección SIP del otro usuario de prueba) y ReceiverCredential (el objeto de Windows PowerShell que contiene las credenciales del otro usuario).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descripción detallada

El cmdlet **Test-CsIM** es un ejemplo de una "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la Red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Normalmente, las transacciones sintéticas se llevan a cabo de dos modos distintos. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar un usuario de prueba para cada grupo de registrador. Estos usuarios de prueba son un par de usuarios que han sido preconfigurados para usar transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas pertenecientes a usuarios reales). Con los usuarios de prueba configurados para un grupo, los administradores simplemente pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

De forma alternativa, los administradores pueden ejecutar una transacción sintética con cuentas de usuarios reales. Por ejemplo, si un usuario no puede intercambiar mensajes instantáneos con otro, un administrador puede ejecutar una transacción sintética con las dos cuentas de usuario en cuestión (en lugar de dos cuentas de prueba) y tratar de diagnosticar y resolver el problema. Si decide llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar las credenciales de cada usuario.

El cmdlet **Test-CsIM** primero intenta iniciar la sesión de un par de usuarios de prueba en Lync Server. Si los dos inicios de sesión se realizan correctamente, el cmdlet inicia una sesión de mensajería instantánea entre los dos usuarios de prueba. (El Usuario 1 invita al Usuario 2 a una sesión de mensajería instantánea y el Usuario 2 acepta la invitación). Después de comprobar que pueden intercambiarse mensajes entre los dos usuarios, el cmdlet **Test-CsIM** finaliza la sesión de mensajería instantánea y cierra la sesión de ambos usuarios en el sistema.

Quiénes pueden ejecutar este cmdlet: Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsIM"}

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credencial de usuario para la primera de las cuentas de usuario que se someterán a prueba. El valor enviado a ReceiverCredential debería ser una referencia a objeto obtenida mediante el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\pilar y almacena dicho objeto en una variable llamada $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Deberá proporcionar la contraseña de usuario cuando ejecuta este comando.</p>
<p>La credencial del receptor no es obligatoria si ejecuta la prueba con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credencial de usuario para la segunda de las cuentas de usuario que se someterán a prueba. El valor enviado a SenderCredential debería ser una referencia a objeto obtenida mediante el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credencial para el usuario litwareinc\kenmyer y almacena ese objeto en una variable denominada $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Deberá proporcionar la contraseña de usuario cuando ejecuta este comando.</p>
<p>La credencial del remitente no es obligatoria si ejecuta la prueba con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>String</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo de servidores que se probará.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación usado en la prueba. Los valores permitidos son:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>EmailHost</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Host de correo electrónico para el usuario empleado en la prueba Legal Intercept. Por ejemplo:</p>
<p>-EmailHost &quot;litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan producirse al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>IsSsl</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Cuando se establece en True, especifica que dicha prueba se lleva a cabo mediante el protocolo de capa de sockets seguros (SSL).</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Cuando esté presente, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Esta variable incluye un par de métodos (ToHTML y ToXML) que después se pueden utilizar para guardar los resultados en un archivo HTML o XML.</p>
<p>Para almacenar resultados en una variable de registrador llamada $TestOutput, utilice la sintaxis siguiente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: no anteponga un carácter $ al especificar el nombre de variable. Para guardar la información almacenada en la variable de registrador en un archivo HTML, utilice un comando similar al siguiente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Para guardar en un archivo XML la información almacenada en la variable de registrador, use un comando similar a este:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Cuando esté presente, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Por ejemplo, para almacenar resultados en una variable llamada $TestOutput, utilice la sintaxis siguiente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>No anteponga un carácter $ al especificar el nombre de variable.</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Contraseña para los empleados en la prueba Legal Intercept.</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>Opcional</p></td>
<td><p>UInt16</p></td>
<td><p>Puerto utilizado para el servicio Legal Intercept.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Dirección SIP de la primera cuenta de usuario que se someterá a prueba. Por ejemplo: -ReceiverSipAddress &quot;sip:jhaas@litwareinc.com&quot;. El parámetro ReceiverSipAddress debe hacer referencia a la misma cuenta de usuario que ReceiverCredential.</p>
<p>La dirección SIP no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Puerto SIP usado por el servicio de registrador. Este parámetro no es obligatorio si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Dirección SIP de la segunda cuenta de usuario que se someterá a prueba. Por ejemplo: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro SenderSipAddress debe referirse a la misma cuenta de usuario que SenderCredential.</p>
<p>La dirección SIP no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestLegalIntercept</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Cuando se utiliza, indica a Test-CsIM que pruebe el servicio Legal Intercept para el usuario especificado.</p></td>
</tr>
<tr class="even">
<td><p><em>Username</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Nombre de usuario del usuario empleado en la prueba Legal Intercept.</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitSeconds</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int16</p></td>
<td><p>Especifica la cantidad de tiempo (en segundos) que el sistema debe esperar a que el servicio Legal Intercept responda.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsIM** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsIM** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsGroupIM](test-csgroupim.md)

