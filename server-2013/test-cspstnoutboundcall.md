---
title: Test-CsPstnOutboundCall
TOCTitle: Test-CsPstnOutboundCall
ms:assetid: 12d940c3-8526-4c8f-8dc1-3fe65a3211bc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398207(v=OCS.15)
ms:contentKeyID: 48274497
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnOutboundCall

 

_**Última modificación del tema:** 2015-03-09_

Comprueba la capacidad de un usuario para realizar una llamada a un número telefónico ubicado en la red telefónica conmutada (RTC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsPstnOutboundCall -TargetPstnPhoneNumber <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall -TargetFqdn <String> -TargetPstnPhoneNumber <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se comprueba si un usuario de prueba preconfigurado pueden iniciar sesión en el grupo atl-cs-001.litwareinc.com y luego hacer una llamada telefónica a través de la puerta de enlace RTC. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. Si se han definido, el comando determinará si el primer usuario de prueba puede iniciar sesión en el sistema y, en caso afirmativo, si puede realizar una llamada telefónica a un teléfono ubicado en la RTC.

Si no se han definido usuarios de prueba, el comando producirá un error porque no sabrá qué usuario emplear al realizar la prueba. Si no se han definido usuarios de prueba para un grupo, deberá incluir el parámetro UserSipAddress además de las credenciales correspondientes a la cuenta de usuario involucrada en la prueba. El cmdlet **Test-CsPstnOutboundCall** después realizará sus comprobaciones con el usuario especificado.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" 

## EJEMPLO 2

Los comandos que se muestran en el ejemplo 2 prueban la capacidad de un usuario de prueba (litwareinc\\kenmyer) de iniciar sesión en Lync Server y luego realizar una llamada telefónica por la puerta de enlace RTC. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Ken Myer. (Dado que el nombre de inicio de sesión, litwareinc\\kenmyer, se ha incluido como parámetro, el cuadro de diálogo de solicitud de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Ken Myer). Luego, el objeto de credenciales resultante se almacena en una variable denominada $cred1.

Con el objeto de credencial en mano, el segundo comando del ejemplo determina si el usuario de prueba puede iniciar sesión o no en Lync Server y después realizar una llamada al número telefónico de destino (+15551234567). Para llevar a cabo esta tarea, se llama al cmdlet **Test-CsPstnOutboundCall** junto con los siguientes parámetros: TargetFqdn (el FQDN del grupo de registradores), UserSipAddress (la dirección SIP del usuario que realiza la llamada), UserCredential (el objeto de Windows PowerShell que contiene las credenciales del usuario de prueba) y TargetPstnPhoneNumber (el número de teléfono al que se llama).

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## EJEMPLO 3

En el ejemplo 3 se muestra cómo se puede usar el cmdlet **Test-CsPstnOutboundCall** en modo de plataforma de servidor. En este modo, se especifica la dirección SIP del usuario, pero no se incluyen las credenciales de usuario. Cuando se ejecuta de esta manera, Lync Server usa certificados para autenticar el usuario de prueba.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress sip:kenmyer@litwareinc.com -TargetPstnPhoneNumber "+15551234567"

## Descripción detallada

El cmdlet **Test-CsPstnOutboundCall** es un ejemplo de una "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la Red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Normalmente, las transacciones sintéticas se llevan a cabo de dos modos distintos. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar un usuario de prueba para cada grupo de registrador. Estos usuarios de prueba son un par de usuarios que han sido preconfigurados para usar transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas pertenecientes a usuarios reales). Con los usuarios de prueba configurados para un grupo, los administradores simplemente pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

De forma alternativa, los administradores pueden ejecutar una transacción sintética con cuentas de usuarios reales. Por ejemplo, si un usuario no puede intercambiar mensajes instantáneos con otro, un administrador puede ejecutar una transacción sintética con las dos cuentas de usuario en cuestión (en lugar de dos cuentas de prueba) y tratar de diagnosticar y resolver el problema. Si decide llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar los nombres de usuario y las contraseñas de cada usuario.

También se puede usar Test-CsPstnOutboundCall en modo de plataforma de servidores. En ese caso, solo necesita especificar la dirección SIP de usuario y Lync Server usará certificados para autenticar ese usuario.

Al ejecutar el cmdlet **Test-CsPstnOutboundCall**, este primero intenta iniciar la sesión del usuario de prueba en Lync Server. Si el inicio de sesión se realiza correctamente, el cmdlet intentará realizar una llamada telefónica mediante la puerta de enlace RTC. Esta llamada telefónica puede realizarse con el plan de marcado, la directiva de voz y con otras directivas y configuraciones asignadas a la cuenta de prueba. Cuando se responde la llamada, el cmdlet envía códigos de tono de marcado de frecuencia múltiple (DTMF) a través de la red a fin de comprobar la conectividad de medios.

Al llevar a cabo la prueba, el cmdlet **Test-CsPstnOutboundCall** realizará una llamada telefónica real: el teléfono de destino sonará y deberá ser atendido para que la prueba sea correcta. Además, el administrador debe finalizar esta llamada manualmente.

Quiénes pueden ejecutar este cmdlet: Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnOutboundCall"}

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
<td><p>String</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo de servidores que se probará.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>String</p></td>
<td><p>Número telefónico RTC al que se llamará durante la realización de la prueba. El número telefónico de destino se especifica mejor al usar el formato E.164, que significa que el número se verá algo así como &quot;+14255551298&quot; y ese número contendrá un signo positivo (+) seguido del código de llamada del país/región (1), el código de área (425) y el número de teléfono (5551298). Al especificar el número telefónico, no use guiones, paréntesis ni ningún otro carácter.</p>
<p>Si no usa el formato E.164, el plan de marcado del usuario de prueba se anexará al número. Lync Server después usará el plan de marcado para normalizar el número con el formato E.164. Si no se puede normalizar el número, no se puede realizar la llamada y la prueba generará un error.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credenciales de usuario de la cuenta de usuario que se someterá a prueba. El valor enviado a UserCredential debería ser una referencia a objeto obtenida mediante el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales para el usuario litwareinc\kenmyer y almacena ese objeto en una variable denominada $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Deberá proporcionar la contraseña de usuario cuando ejecuta este comando.</p>
<p>Este parámetro no es necesario si el comando emplea usuarios de prueba configurados al usar los cmdlets CsHealthMonitoringConfiguration. Además no necesita especificar este parámetro si la prueba se realiza en modo de plataforma de servidor. En ese caso, Lync Server intentará autenticar al usuario con el uso de certificados.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación usado en la prueba. Los valores permitidos son:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan producirse al ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Cuando esté presente, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Esta variable incluye un par de métodos (ToHTML y ToXML) que después se pueden utilizar para guardar los resultados en un archivo HTML o XML.</p>
<p>Para almacenar resultados en una variable de registrador llamada $TestOutput, utilice la sintaxis siguiente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: no anteponga un carácter $ al especificar los nombres de variable. Para guardar en un archivo HTML la información almacenada en la variable de registrador, use un comando similar a este:</p>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Puerto SIP usado por el servicio de registrador. Este parámetro no es obligatorio si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Dirección SIP de la cuenta de usuario que se someterá a prueba. Por ejemplo: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro UserSipAddress debe hacer referencia a la misma cuenta de usuario que UserCredential.</p>
<p>Este parámetro no es necesario si el comando emplea usuarios de prueba configurados al usar los cmdlets CsHealthMonitoringConfiguration.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsPstnOutboundCall** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsPstnOutboundCall** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md)

