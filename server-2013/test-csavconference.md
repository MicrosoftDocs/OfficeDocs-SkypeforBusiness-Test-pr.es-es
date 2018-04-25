---
title: Test-CsAVConference
TOCTitle: Test-CsAVConference
ms:assetid: a1492563-9a97-44ac-b19a-8d5972cdd062
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412749(v=OCS.15)
ms:contentKeyID: 48276168
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAVConference

 

_**Última modificación del tema:** 2015-03-09_

Comprueba la capacidad de que un par de usuarios participen en una conferencia de audio o vídeo (A/V). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsAVConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAVConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAVConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Ejemplos

## Ejemplo 1

En el ejemplo anterior se comprueba si un par de usuarios de prueba preconfigurados pueden iniciar sesión en el grupo de servidores atl-cs-001.litwareinc.com y luego participar en una conferencia de A/V. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. Si es así, el comando determinará si los dos usuarios pueden iniciar sesión en el sistema. En caso afirmativo, el primer usuario de prueba creará una conferencia de A/V e invitará al segundo a participar; a continuación, el cmdlet comprobará si los dos usuarios han podido establecer conexión correctamente o no.

Si no se definieron usuarios de prueba, el comando producirá un error porque no sabrá qué usuarios emplear para realizar la prueba. Si no definió ningún usuario de prueba para el grupo, deberá incluir los parámetros SenderSipAddress y ReceiverSipAddress, además de las credenciales correspondientes a los usuarios implicados en el intercambio de mensajes instantáneos. Luego, el cmdlet **Test-CsAVConference** realizará las comprobaciones con los dos usuarios especificados.

    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com 

## Ejemplo 2

Los comandos que se muestran en el ejemplo 2 prueban la capacidad de un par de usuarios (litwareinc\\pilar y litwareinc\\kenmyer) de iniciar sesión en Lync Server y participar en una conferencia de A/V. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de petición de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). El objeto de credenciales resultante se almacena a continuación en una variable llamada $cred1. El segundo comando realiza la misma acción pero, esta vez, devuelve un objeto de credenciales de la cuenta de Ken Myer.

Con ambos objetos de credenciales en mano, el tercer comando del ejemplo determina si los dos usuarios pueden iniciar sesión en Lync Server y luego participar en una conferencia de A/V. Para llevar a cabo esta tarea, se llama al cmdlet **Test-CsAVConference** con los siguientes parámetros: TargetFqdn (el FQDN del grupo de registradores); SenderSipAddress (la dirección SIP del primer usuario de prueba); SenderCredential (el objeto de Windows PowerShell que contiene las credenciales de este mismo usuario); ReceiverSipAddress (la dirección SIP del otro usuario de prueba) y ReceiverCredential (el objeto de Windows PowerShell que contiene las credenciales del otro usuario).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descripción detallada

El cmdlet **Test-CsAVConference** es un ejemplo de "transacción sintética". Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios puedan completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o hacer llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede iniciarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Las transacciones sintéticas se suelen llevar a cabo de dos formas. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar usuarios de prueba para cada grupo de registradores. Estos usuarios de prueba son un par de usuarios preconfigurados para usar transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas de usuarios reales). Con los usuarios de prueba configurados para un grupo de servidores, los administradores pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

También es posible ejecutar una transacción sintética con cuentas de usuario reales. Por ejemplo, si dos usuarios no pueden intercambiar mensajes instantáneos, un administrador puede ejecutar una transacción sintética con esas dos cuentas de usuario (en lugar de dos cuentas de prueba) e intentar diagnosticar y resolver el problema. Para llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar los nombres de usuario y las contraseñas de cada usuario.

El cmdlet **Test-CsAVConference** comprueba si dos usuarios de prueba pueden mantener una conferencia de A/V. Cuando se ejecuta el cmdlet, los dos usuarios ya deben haber iniciado sesión en el sistema. Con la sesión correctamente iniciada, el primer usuario crea una conferencia de A/V y, entonces, espera a que el segundo usuario se una a esa misma conferencia. Después de un breve intercambio de datos, la conferencia se elimina y los dos usuarios de prueba finalizan la sesión.

El cmdlet **Test-CsAVConference** no realiza, en realidad, una conferencia de A/V entre dos usuarios de prueba, simplemente comprueba que los dos usuarios puedan realizar las conexiones necesarias para llevar a cabo la conferencia de A/V.

Quién puede iniciar este cmdlet: Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAVConference"}

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
<td><p>El objeto de credenciales de usuario correspondiente a la primera de las dos cuentas de usuario que se pondrán a prueba. El valor transferido a ReceiverCredential debe ser una referencia a objeto obtenida con el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\pilar y almacena dicho objeto en una variable llamada $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Debe facilitar la contraseña de usuario al iniciar este comando.</p>
<p>La credencial del receptor no es obligatoria si ejecuta la prueba con las opciones de configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>El objeto de credenciales de usuario correspondiente a la segunda de las dos cuentas de usuario que se pondrán a prueba. El valor transferido a SenderCredential debe ser una referencia a objeto obtenida con el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\kenmyer y almacena dicho objeto en una variable llamada $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Debe facilitar la contraseña de usuario al iniciar este comando.</p>
<p>La credencial del remitente no es obligatoria si ejecuta la prueba con las opciones de configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Cadena</p></td>
<td><p>Nombre de dominio completo (FQDN) del grupo de servidores que se probará.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Si está presente, el resultado detallado de iniciar el cmdlet se almacenará en la variable especificada. Por ejemplo, para almacenar resultados en una variable llamada $TestOutput, use la sintaxis siguiente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>No anteponga un carácter $ al especificar el nombre de variable.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección SIP de la primera de las dos cuentas de usuario que se pondrán a prueba. Por ejemplo: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. El parámetro ReceiverSipAddress debe hacer referencia a la misma cuenta de usuario que ReceiverCredential.</p>
<p>La dirección SIP no es obligatoria si se ejecuta la prueba con las opciones de configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Puerto SIP usado por el servicio registrador. Este parámetro no es obligatorio si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección SIP de la segunda de las dos cuentas de usuario que se pondrán a prueba. Por ejemplo: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro SenderSIPAddress debe referirse a la misma cuenta de usuario que SenderCredential.</p>
<p>La dirección SIP no es obligatoria si se inicia la prueba con las opciones de configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Si está presente, comprueba la capacidad de Join Launcher para participar en una conferencia de audio y vídeo. Join Launcher se usa para ayudar a los usuarios de dispositivos móviles (es decir, a los usuarios del servicio de movilidad) a participar en conferencias.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Test-CsAVConference** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[Test-CsDialInConferencing](test-csdialinconferencing.md)

