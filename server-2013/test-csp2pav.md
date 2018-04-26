---
title: Test-CsP2PAV
TOCTitle: Test-CsP2PAV
ms:assetid: acb01fb7-4685-4f38-a724-8c2ae8e0219a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412821(v=OCS.15)
ms:contentKeyID: 48276340
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsP2PAV

 

_**Última modificación del tema:** 2015-03-09_

Comprueba la capacidad de dos usuarios para realizar una llamada de audio y vídeo (A/V) de punto a punto. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsP2PAV -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsP2PAV -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsP2PAV [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Ejemplos

## Ejemplo 1

En el ejemplo anterior se comprueba que un par de usuarios de prueba preconfigurados pueden iniciar sesión en el grupo atl-cs-001.litwareinc.com y realizar una llamada de audio y vídeo de punto a punto. Este comando solo funcionará si se han definido usuarios de prueba para el grupo de servidores atl-cs-001.litwareinc.com. En caso afirmativo, el comando determinará si los dos usuarios pueden iniciar sesión en el sistema y, en caso de que así sea, sí pueden conversar con una llamada de audio y vídeo.

Si no se definieron usuarios de prueba, el comando producirá un error porque no sabrá qué usuarios emplear para realizar la prueba. Si no definió ningún usuario de prueba para el grupo, deberá incluir los parámetros SenderSipAddress y ReceiverSipAddress, además de las credenciales correspondientes a los usuarios implicados en el intercambio de mensajes instantáneos. Luego, el cmdlet **Test-CsP2PAV** realizará las comprobaciones con los dos usuarios especificados.

    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com 

## Ejemplo 2

Los comandos del ejemplo 2 comprueban la capacidad de un par de usuarios (litwareinc\\pilar y litwareinc\\kenmyer) para iniciar sesión en Lync Server y, a continuación, realizan una llamada de A/V. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de petición de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). El objeto de credenciales resultante se almacena a continuación en una variable llamada $cred1. El segundo comando realiza la misma acción pero, esta vez, devuelve un objeto de credenciales de la cuenta de Ken Myer.

Con los dos objetos de credenciales a mano, el tercer comando del ejemplo determina si los dos usuarios pueden iniciar sesión en Lync Server y realizar una llamada de audio y vídeo de punto a punto. Para llevar a cabo esta tarea, se llama al cmdlet **Test-CsP2PAV** y a los parámetros siguientes: TargetFqdn (el FQDN del grupo de registradores); SenderSipAddress (la dirección SIP del primer usuario de prueba); SenderCredential (el objeto de Windows PowerShell que contiene las credenciales de este mismo usuario); ReceiverSipAddress (la dirección SIP del otro usuario de prueba) y ReceiverCredential (el objeto de Windows PowerShell que contiene las credenciales del otro usuario).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descripción detallada

El cmdlet **Test-CsP2PAV** es un ejemplo de "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede iniciarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Las transacciones sintéticas se suelen llevar a cabo de dos formas. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar usuarios de prueba para cada grupo de registradores. Estos usuarios de prueba son un par de usuarios preconfigurados para usar transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas de usuarios reales). Con los usuarios de prueba configurados para un grupo de servidores, los administradores pueden sencillamente ejecutar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

Por otra parte, los administradores pueden optar por ejecutar una transacción sintética con cuentas de usuario reales. Por ejemplo, si dos usuarios no pueden intercambiar mensajes instantáneos, un administrador puede ejecutar una transacción sintética con las dos cuentas de usuario en cuestión (en lugar de dos cuentas de prueba) e intentar diagnosticar y resolver el problema. Para llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar los nombres de usuario y las contraseñas de cada usuario.

El cmdlet **Test-CsP2PAV** se usa para determinar si dos usuarios de prueba pueden participar en una conversación de audio y vídeo (A/V) de punto a punto. Para probar este escenario, el cmdlet comienza por registrar los dos usuarios en Lync Server. Supongamos que los dos inician sesión correctamente, el primer usuario invita al segundo a unirse a una llamada de A/V. El segundo usuario acepta la llamada y se prueba la conexión entre ambos. Luego, la llamada finaliza y los usuarios cierran sesión en el sistema.

En realidad, el cmdlet **Test-CsP2PAV** no realiza una llamada de A/V; la información multimedia no se intercambia entre los usuarios de prueba. En su lugar, el cmdlet tan solo comprueba que se establezcan las conexiones correspondientes y que los dos usuarios puedan mantener este tipo de llamada.

Quién puede iniciar este cmdlet: Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsP2PAV"}

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
<td><p>Dirección SIP de la segunda de las dos cuentas de usuario que se pondrán a prueba. Por ejemplo: -SenderSipAddres &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro SenderSipAddress debe referirse a la misma cuenta de usuario que SenderCredential.</p>
<p>La dirección SIP no es obligatoria si se ejecuta la prueba con las opciones de configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsP2PAV** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsP2PAV** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsAVConference](test-csavconference.md)

