---
title: Test-CsGroupIM
TOCTitle: Test-CsGroupIM
ms:assetid: 1e73fd7a-5727-4688-8d4c-a3107c3985e9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398273(v=OCS.15)
ms:contentKeyID: 48274619
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupIM

 

_**Última modificación del tema:** 2015-03-09_

Prueba la capacidad de dos usuarios de realizar una conferencia de mensajería instantánea (MI). El cmdlet **Test-CsGroupIM** es una "transacción sintética", es decir, una simulación de actividades comunes de Lync Server usadas para el seguimiento de estado y la supervisión de rendimiento. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsGroupIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se comprueba si un par de usuarios de prueba preconfigurados pueden iniciar sesión en el grupo atl-cs-001.litwareinc.com y participar en una conferencia de mensajería instantánea. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. Si es así, el comando determinará si ambos usuarios pueden iniciar sesión en el sistema y, a continuación, comprobará si pueden participar en una conferencia de mensajería instantánea.

Si no se han definido usuarios de prueba, se producirá un error en el comando porque no sabrá qué usuario emplear para realizar la prueba. Si no se han definido usuarios de prueba para un grupo, deberá incluir los parámetros SenderSipAddress y ReceiverSipAddress, y las credenciales correspondientes de los usuarios implicados en la sesión de mensajería instantánea. A continuación, el cmdlet **Test-CsGroupIM** realizará sus comprobaciones con los dos usuarios especificados.

    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com

## EJEMPLO 2

Los comandos que se muestran en el ejemplo 2 prueban la capacidad de un par de usuarios (litwareinc\\pilar y litwareinc\\kenmyer) de iniciar sesión en Lync Server, y, a continuación, participar en una conferencia de mensajería instantánea Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de solicitud de credenciales resultante de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). Luego, el objeto de credenciales resultante se almacena en una variable denominada $cred1. El segundo comando hace lo mismo, pero devuelve un objeto de credenciales para la cuenta de Ken Myer.

Con ambos objetos credencial en mano, el tercer comando del ejemplo determina si los dos usuarios pueden o no iniciar sesión en Lync Server y participar en una conferencia de mensajería instantánea. Para llevar a cabo esta tarea, se llama al cmdlet **Test-CsGroupIM** junto con los siguientes parámetros: TargetFqdn (el FQDN del grupo de registradores), SenderSipAddress (la dirección SIP del primer usuario), SenderCredential (las credenciales de usuario del primer usuario), ReceiverSipAddress (la dirección SIP del segundo usuario) y ReceiverCredential (las credenciales de usuario del segundo usuario).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descripción detallada

El cmdlet **Test-CsGroupIM** es un ejemplo de una transacción sintética de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la Red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Normalmente, las transacciones sintéticas se llevan a cabo de dos modos distintos. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar un usuario de prueba para cada grupo de registrador. Estos usuarios de prueba son un par de usuarios que han sido preconfigurados para usar transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas pertenecientes a usuarios reales). Con los usuarios de prueba configurados para un grupo, los administradores simplemente pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

De forma alternativa, los administradores pueden ejecutar una transacción sintética con cuentas de usuarios reales. Por ejemplo, si dos usuarios no pueden intercambiar mensajes instantáneos, un administrador puede ejecutar una transacción sintética con las cuentas de dichos usuarios (en lugar de dos cuentas de prueba) y, a continuación, intentar diagnosticar y resolver el problema. Si decide llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar las credenciales de cada usuario.

El cmdlet **Test-CsGroupIM** le permite comprobar que los usuarios de la organización pueden realizar conferencias. El cmdlet **Test-CsGroupIM** requiere dos cuentas de usuario para llevar a cabo sus pruebas. Si ha configurado usuarios de prueba para el grupo donde se realizará la prueba, no necesita especificar las cuentas; el cmdlet **Test-CsGroupIM** usará automáticamente las cuentas de prueba asignadas al grupo. (Para obtener más información, consulte el tema de ayuda del cmdlet [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)). También puede llevar a cabo la prueba con cuentas distintas de las asignadas al registrador. Esto le permitirá ejecutar pruebas aún sin haber configurado usuarios de prueba para el grupo. También le permite comprobar la capacidad de dos usuarios específicos para realizar una conferencia. Si decide usar este método, deberá proporcionar el nombre de usuario y la contraseña de ambos usuarios.

Al ejecutar el cmdlet **Test-CsGroupIM**, este intenta iniciar la sesión de ambos usuarios de prueba en Lync Server. Si el resultado es correcto, el cmdlet **Test-CsGroupIM** crea una nueva conferencia con el primer usuario de prueba y, a continuación, invita al segundo usuario a unirse a ella. Después de un intercambio de mensajes, se desconectan ambos usuarios del sistema. Todo esto ocurre sin la interacción del usuario y sin afectar a los usuarios reales. Por ejemplo, supongamos que la cuenta de prueba sip:kenmyer@litwareinc.com corresponde a un usuario real con una cuenta real de Lync Server. En ese caso, la prueba se realizará sin ningún tipo de interrupción ocasionada al Ken Myer real. Por ejemplo, aunque la cuenta de prueba de Ken Myer cierre sesión en el sistema, el usuario Ken Myer permanecerá conectado. De manera similar, el usuario Ken Myer real no recibirá ninguna invitación a unirse a la conferencia. Dicha invitación se enviará a la cuenta de prueba y esta la aceptará.

Agregar el parámetro Verbose le permitirá obtener una cuenta detallada de las acciones realizadas por el cmdlet **Test-CsGroupIM** para finalizar su prueba.

Quiénes pueden ejecutar este cmdlet: Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupIM"}

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
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan producirse al ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
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
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Dirección SIP de la primera cuenta de usuario que se someterá a prueba. Por ejemplo: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. El parámetro ReceiverSipAddress debe hacer referencia a la misma cuenta de usuario que ReceiverCredential.</p>
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
<td><p>Dirección SIP de la segunda de las dos cuentas de usuario que se pondrán a prueba. Por ejemplo: -SenderSipAddres &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro ReceiverSipAddress debe hacer referencia a la misma cuenta de usuario que SenderCredential.</p>
<p>La dirección SIP no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Cuando está presente, prueba la capacidad del Iniciador de participación en reuniones de participar en una conferencia de audio y vídeo. El Iniciador de participación en reuniones se usa para ayudar a los usuarios de dispositivos móviles (y, por consiguiente, a los usuarios del servicio de movilidad) a participar en conferencias.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsGroupIM** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsGroupIM** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsIM](test-csim.md)

