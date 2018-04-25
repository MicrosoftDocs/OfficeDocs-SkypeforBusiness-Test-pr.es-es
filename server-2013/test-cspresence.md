---
title: Test-CsPresence
TOCTitle: Test-CsPresence
ms:assetid: 09a5faf6-4e80-4a3b-ac84-aec9778ee9b5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398148(v=OCS.15)
ms:contentKeyID: 48274366
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPresence

 

_**Última modificación del tema:** 2015-03-09_

Prueba la capacidad de un usuario de iniciar sesión en Lync Server, publicar su información de presencia y, luego, suscribirse a la información de presencia publicada por un segundo usuario. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsPresence -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-PublisherSipAddress <String>] [-RegistrarPort <Int32>] [-SubscriberSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPresence -PublisherCredential <PSCredential> -PublisherSipAddress <String> -SubscriberCredential <PSCredential> -SubscriberSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPresence [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-SubscriberSipAddress <String>]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1 se comprueba si un par de usuarios de prueba preconfigurados pueden iniciar sesión en el grupo atl-cs-001.litwareinc.com. Una vez que los usuarios de prueba inician sesión, el cmdlet **Test-CsPresence** comprueba si los dos usuarios pueden intercambiar información de presencia. Este comando solo funcionará si se han definido usuarios de prueba para el grupo atl-cs-001.litwareinc.com. Si es así, el comando determinará si el primer usuario de prueba puede iniciar sesión en el sistema y luego comprobará si este usuario puede intercambiar información de presencia con el segundo usuario de prueba definido para el grupo.

Si no se ha definido ningún registrador, el comando no funcionará porque no sabrá qué usuarios debe emplear al realizar la prueba. Si no ha definido usuarios de prueba para un grupo de servidores, deberá incluir los parámetros SubscriberSipAddress y PublisherSipAddress además de las credenciales correspondientes para los usuarios que actúan como suscriptor y publicador de presencia. El cmdlet **Test-CsPresence** después realizará sus comprobaciones con los dos usuarios especificados.

    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com 

## EJEMPLO 2

Los comandos que se muestran en el ejemplo 2 prueban la capacidad de un par de usuarios (litwareinc\\pilar y litwareinc\\kenmyer) de iniciar sesión en Lync Server, y después intercambiar información de presencia. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de solicitud de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). Luego, el objeto de credenciales resultante se almacena en una variable denominada $cred1. El segundo comando hace lo mismo, pero devuelve un objeto de credenciales para la cuenta de Ken Myer.

Con ambos objetos credencial en mano, el tercer comando del ejemplo determina si los dos usuarios pueden o no iniciar sesión en Lync Server e intercambiar información de presencia. Para llevar a cabo esta tarea, se llama al cmdlet **Test-CsPresence** con los siguientes parámetros: TargetFqdn (el FQDN del grupo de registradores), SubscriberSipAddress (la dirección SIP de un usuario de prueba), SubscriberCredential (el objeto de Windows PowerShell que contiene las credenciales de este mismo usuario), PublisherSipAddress (la dirección SIP del otro usuario de prueba) y PublisherCredential (el objeto de Windows PowerShell que contiene las credenciales del otro usuario).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com -SubscriberSipAddress "sip:pilar@litwareinc.com" -SubscriberCredential $cred1 -PublisherSipAddress "sip:kenmyer@litwareinc.com" -PublisherCredential $cred2

## Descripción detallada

El cmdlet **Test-CsPresence** es un ejemplo de una transacción sintética de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la Red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede ejecutarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Normalmente, las transacciones sintéticas se llevan a cabo de dos modos distintos. Muchos administradores usarán los cmdlets **CsHealthMonitoringConfiguration** para configurar a los usuarios de prueba para cada grupo de registrador. Normalmente se usan cuentas de prueba, no cuentas de usuarios reales. Con estas cuentas de usuarios configuradas para un grupo, los administradores simplemente pueden ejecutar una transacción sintética en dicho grupo sin tener que especificar las identidades de las cuentas de usuario implicadas en la prueba, ni facilitar sus credenciales.

De forma alternativa, los administradores pueden ejecutar una transacción sintética con cuentas de usuarios reales. Por ejemplo, si un usuario no puede intercambiar mensajes instantáneos con otro, un administrador puede ejecutar una transacción sintética con las dos cuentas de usuario en cuestión (en lugar de dos cuentas de prueba) y tratar de diagnosticar y resolver el problema. Si decide llevar a cabo una transacción sintética con cuentas de usuario reales, deberá especificar los nombres de usuario y las contraseñas de cada usuario.

El cmdlet **Test-CsPresence** se usa para determinar si un par de usuarios de prueba puede iniciar sesión en Lync Server y, luego, intercambiar información de presencia. Para esto, el cmdlet primero inicia la sesión de ambos usuarios en el sistema. Si los dos inicios de sesión se realizan correctamente, el primer usuario de prueba solicita recibir información de presencia del segundo usuario. El segundo usuario publica esta información y el cmdlet **Test-CsPresence** comprueba que esta se transmita correctamente al primer usuario. Después de que intercambian información de presencia, se cierra la sesión de Lync Server de los dos usuarios de prueba.

Quiénes pueden ejecutar este cmdlet: Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPresence"}

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
<td><p><em>PublisherCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credencial de usuario para la primera de las cuentas de usuario que se someterán a prueba. El valor enviado a PublisherCredential debería ser una referencia a objeto obtenida mediante el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credencial para el usuario litwareinc\kenmyer y almacena ese objeto en una variable denominada $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Deberá proporcionar la contraseña de usuario cuando ejecuta este comando.</p>
<p>La credencial del publicador no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado para el grupo.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credencial de usuario para la segunda de las cuentas de usuario que se someterán a prueba. El valor enviado a SubscriberCredential debería ser una referencia a objeto obtenida mediante el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credenciales del usuario litwareinc\pilar y almacena dicho objeto en una variable llamada $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Deberá proporcionar la contraseña de usuario cuando ejecuta este comando.</p>
<p>La credencial del suscriptor no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado para el grupo.</p></td>
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
<td><p>Tipo de autenticación que se usa en la prueba. Los valores permitidos son:</p>
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
<td><p><em>PublisherSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Dirección SIP de la primera cuenta de usuario que se someterá a prueba. Por ejemplo: -PublisherSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro PublisherSipAddress debe hacer referencia a la misma cuenta de usuario que PublisherCredential.</p>
<p>La dirección SIP no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Puerto SIP usado por el servicio de registrador. Este parámetro no es obligatorio si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Dirección SIP de la segunda cuenta de usuario que se someterá a prueba. Por ejemplo: -SubscriberSipAddress &quot;sip:pilar@litwareinc.com&quot;. El parámetro SubscriberSipAddress debe hacer referencia a la misma cuenta de usuario que SubscriberCredential.</p>
<p>La dirección SIP no es obligatoria si la prueba se ejecuta con la configuración de seguimiento de estado del grupo.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsPresence** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsPresence** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Test-CsRegistration](test-csregistration.md)

