---
title: Test-CsPstnPeerToPeerCall
TOCTitle: Test-CsPstnPeerToPeerCall
ms:assetid: 839cf83f-b667-4cbe-b1ab-28f54a8a9d0b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398662(v=OCS.15)
ms:contentKeyID: 48275880
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnPeerToPeerCall

 

_**Última modificación del tema:** 2015-03-09_

Prueba la capacidad de un par de usuarios para hacer una llamada de punto a punto con la puerta de enlace de la red telefónica conmutada (RTC). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsPstnPeerToPeerCall -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Ejemplos

## Ejemplo 1

En el ejemplo 1 se comprueba si un par de usuarios de prueba preconfigurados puede iniciar sesión en el grupo atl-cs-001.litwareinc.com. Una vez que hayan iniciado sesión, el cmdlet **Test-CsPstnPeerToPeerCall** comprueba si ambos usuarios pueden hacer una llamada de punto a punto con la puerta de enlace de RTC. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. Si es así, el comando averiguará si el primer usuario de prueba puede iniciar sesión en el sistema y después si este usuario puede llamar al segundo usuario definido del grupo.

Si no se ha definido ningún usuario de prueba, el comando producirá un error porque no sabrá qué usuarios emplear para llevar a cabo la prueba. Si no ha definido usuarios de prueba para un grupo y no está trabajando en modo de plataforma de servidores, tendrá que incluir los parámetros SenderSipAddress y ReceiverSipAddress y las credenciales correspondientes para los usuarios que se usarán como cuentas de prueba. Después, el cmdlet **Test-CsPstnPeerToPeerCall** llevará a cabo sus comprobaciones con los dos usuarios especificados.

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com 

## Ejemplo 2

Los comandos del ejemplo 2 comprueban la capacidad de un par de usuarios (litwareinc\\pilar y litwareinc\\kenmyer) para iniciar sesión en Lync Server y, a continuación, hacen una llamada de punto a punto con la puerta de enlace de RTC. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de petición de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). El objeto de credenciales resultante se almacena a continuación en una variable llamada $cred1. El segundo comando realiza la misma acción pero, esta vez, devuelve un objeto de credenciales de la cuenta de Ken Myer.

Con los dos objetos de credenciales, el tercer comando del ejemplo averigua si los dos usuarios pueden iniciar sesión en Lync Server y después hace una llamada de punto a punto con la puerta de enlace de RTC. Para llevar a cabo esta tarea, se llama al cmdlet **Test-CsPstnPeerToPeerCall** junto con los siguientes parámetros: TargetFqdn (el FQDN del grupo de registrador); SenderSipAddress (la dirección SIP del primer usuario de prueba); SenderCredential (el objeto de Windows PowerShell que contiene las credenciales de este mismo usuario); ReceiverSipAddress (la dirección SIP del otro usuario de prueba) y ReceiverCredential (el objeto de Windows PowerShell que contiene las credenciales del otro usuario).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Ejemplo 3

El ejemplo 3 muestra el uso del cmdlet Test-CsPstnPeerToPeerCall en modo de plataforma de servidor. En este modo, se especifican las direcciones SIP de los usuarios de prueba, pero no se incluyen las credenciales de usuario. Cuando se ejecuta así, Lync Server usa certificados para autenticar a los dos usuarios de prueba.

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" 

## Descripción detallada

El cmdlet **Test-CsPstnPeerToPeerCall** es un ejemplo de "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o hacer llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede llevarlas a cabo un administrador de manera manual o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Hay dos métodos para llevar a cabo transacciones sintéticas. Muchos administradores usarán los cmdlet **CsHealthMonitoringConfiguration** para configurar usuarios de prueba para cada grupo de registrador. Los usuarios de prueba son un par de usuarios preconfigurados para usar con transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas de usuarios reales.) Con los usuarios de prueba configurados para un grupo, los administradores pueden ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

Por otra parte, los administradores pueden optar por ejecutar una transacción sintética con cuentas de usuario reales. Por ejemplo, si dos usuarios no pueden intercambiar mensajes instantáneos, un administrador puede ejecutar una transacción sintética con las dos cuentas de usuario en cuestión (en lugar de dos cuentas de prueba) e intentar diagnosticar y resolver el problema. Para llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar los nombres de usuario y las contraseñas de cada usuario.

El cmdlet **Test-CsPstnPeerToPeerCall** también se puede usar en modo de plataforma de servidor. En ese caso, solo será necesario especificar la dirección SIP de los usuarios y Lync Server usará los certificados para autenticar a esos usuarios.

Al llamar al cmdlet **Test-CsPstnPeerToPeerCall**, el cmdlet intentará primero iniciar sesión con los dos usuarios de prueba en Lync Server. Si asumimos que las sesiones se inician correctamente, el cmdlet hará que el usuario 1 intente llamar al usuario 2 con la puerta de enlace de RTC; el cmdlet **Test-CsPstnPeerToPeerCall** hace la llamada con el plan de marcado, la directiva de voz y otras opciones de configuración y directivas asignadas al usuario de prueba. Si la prueba da el resultado esperado, el cmdlet verificará que el usuario 2 pudo responder a la llamada y cerrará la sesión de ambas cuentas en el sistema.

El cmdlet **Test-CsPstnPeerToPeerCall** hace una llamada telefónica real para verificar que la conexión se puede establecer y, además, transmitir códigos de tono de marcado de frecuencia múltiple (DTMF) por toda la red para determinar si se pueden enviar contenidos multimedia a través de la conexión. No obstante, el mismo cmdlet responde a la llamada y no necesita terminación manual. (O sea, no es necesario que nadie responda y cuelgue el teléfono al que se llama).

Quién puede iniciar este cmdlet: para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnPeerToPeerCall"}

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
<p>Las credenciales del receptor no son necesarias si se está iniciando la prueba con las opciones de configuración de supervisión de mantenimiento del grupo o si se está iniciando en modo de plataforma de servidor.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>El objeto de credenciales de usuario correspondiente a la segunda de las dos cuentas de usuario que se pondrán a prueba. El valor transferido a SenderCredential debe ser una referencia a objeto obtenida con el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\kenmyer y almacena dicho objeto en una variable llamada $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Debe facilitar la contraseña de usuario al iniciar este comando.</p>
<p>Las credenciales del remitente no son necesarias si se está ejecutando la prueba con las opciones de configuración de supervisión de mantenimiento del grupo o si se está iniciando en modo de plataforma de servidor.</p></td>
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
<td><p>Dirección SIP de la primera de las dos cuentas de usuario que se pondrán a prueba. Por ejemplo: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. El parámetro ReceiverSIPAddress debe referirse a la misma cuenta de usuario que ReceiverCredential.</p>
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
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsPstnPeerToPeerCall** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsPstnPeerToPeerCall** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsPstnOutboundCall](test-cspstnoutboundcall.md)

