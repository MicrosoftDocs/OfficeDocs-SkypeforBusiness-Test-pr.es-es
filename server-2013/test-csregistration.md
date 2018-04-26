---
title: Test-CsRegistration
TOCTitle: Test-CsRegistration
ms:assetid: 9e38cb36-c97a-43f2-97fe-64759f663be2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412737(v=OCS.15)
ms:contentKeyID: 48276150
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsRegistration

 

_**Última modificación del tema:** 2015-03-09_

Prueba la capacidad del usuario de iniciar sesión en Lync Server. El cmdlet **Test-CsRegistration** es una "transacción sintética": una simulación de actividades comunes de Lync Server usadas para la supervisión del rendimiento y el seguimiento de estado. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsRegistration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsRegistration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsRegistration [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Ejemplos

## Ejemplo 1

En el ejemplo anterior, se prueba el servicio de registrador para el grupo atl-cs-001.litwareinc.com. Este comando solo funcionará si se han definido usuarios de prueba para el grupo atl-cs-001.litwareinc.com. Si es así, el comando determinará si el primer usuario de prueba puede iniciar sesión en Lync Server.

Si no se han definido usuarios de prueba, el comando producirá un error porque no sabrá con qué usuario iniciar sesión. Si no han definido usuarios de prueba para un grupo, deberá incluir el parámetro UserSipAddress y las credenciales del usuario que debe usar el comando al intentar iniciar sesión.

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com 

## Ejemplo 2

Los comandos que se muestran en el ejemplo 2 prueban la capacidad de un usuario específico (litwareinc\\pilar) de iniciar sesión en Lync Server. Para ello, el primer comando del ejemplo usa el cmdlet **Get-Credential** para crear un objeto de credencial de Windows PowerShell con el nombre y la contraseña del usuario Pilar Ackerman. (Dado que el nombre de inicio de sesión, litwareinc\\pilar, se ha incluido como parámetro, el cuadro de diálogo de petición de credenciales de Windows PowerShell pedirá al administrador que escriba únicamente la contraseña de la cuenta de Pilar Ackerman). Luego, el objeto de credencial resultante se almacena en una variable denominada $cred1.

Luego, el segundo comando comprueba si este usuario puede iniciar sesión en el grupo atl-cs-001.litwareinc.com. Para ello, se llama al cmdlet **Test-CsRegistration** con tres parámetros: TargetFqdn (el FQDN del grupo de registradores); UserCredential (el objeto de Windows PowerShell que contiene las credenciales de usuario de Pilar Ackerman); y UserSipAddress (la dirección SIP correspondiente a las credenciales de usuario suministradas).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:pilar@litwareinc.com"

## Descripción detallada

El cmdlet **Test-CsRegistration** es un ejemplo de "transacción sintética" de Lync Server. Las transacciones sintéticas se usan en Lync Server para comprobar que los usuarios pueden completar correctamente tareas comunes, como iniciar sesión en el sistema, intercambiar mensajes instantáneos o realizar llamadas a teléfonos de la red telefónica conmutada (RTC). Estas pruebas puede realizarlas un administrador de manera manual o puede iniciarlas automáticamente una aplicación, como Microsoft System Center Operations Manager (anteriormente Microsoft Operations Manager).

Normalmente, las transacciones sintéticas se llevan a cabo de dos modos distintos. Muchos administradores usarán los cmdlets CsHealthMonitoringConfiguration para configurar usuarios de prueba para cada grupo de registradores. Estos usuarios de prueba son un par de usuarios que se han preconfigurado para usarse con transacciones sintéticas. (Normalmente se usan cuentas de prueba, no cuentas de usuarios reales). Con usuarios de prueba configurados para un grupo, los administradores pueden iniciar una transacción sintética con el grupo, sin necesidad de especificar las identidades, ni suministrar las credenciales, de las cuentas de usuario usadas para la prueba.

De forma alternativa, los administradores pueden iniciar una transacción sintética con cuentas de usuarios reales. Por ejemplo, si un usuario no puede intercambiar mensajes instantáneos con otro, un administrador puede iniciar una transacción sintética con las dos cuentas de usuario en cuestión (en lugar de dos cuentas de prueba) y tratar de diagnosticar y resolver el problema. Tenga en cuenta que para llevar a cabo una transacción sintética con cuentas de usuario reales deberá especificar los nombres de inicio de sesión y las contraseñas de cada usuario.

El cmdlet **Test-CsRegistration** le permite comprobar que los usuarios de su organización pueden iniciar sesión en Lync Server. Para realizar esta comprobación, el cmdlet **Test-CsRegistration** necesita una única cuenta de prueba. Si ha configurado usuarios de prueba para el grupo donde se realizará la prueba, no necesita especificar una cuenta; en su lugar, el cmdlet **Test-CsRegistration** usará automáticamente la primera cuenta de prueba asignada al grupo. (Para más información, vea el tema de ayuda [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md). También puede realizar la prueba con una cuenta que no se haya asignado al grupo. Esto le permitirá iniciar pruebas aun sin haber configurado usuarios de prueba. Asimismo, le permitirá probar la capacidad de un usuario específico para iniciar sesión en Lync Server. (Si elige usar este método, deberá proporcionar el nombre del usuario y la contraseña para la cuenta que se prueba).

Cuando ejecuta **Test-CsRegistration**, el cmdlet intenta que el usuario de prueba inicie sesión en Lync Server y luego si lo logra, desconecta al usuario de prueba del sistema. Todo esto ocurre sin la interacción del usuario y sin afectar a los usuarios reales. Por ejemplo, supongamos que la cuenta de prueba sip:kenmyer@litwareinc.com corresponde a un usuario real con una cuenta real de Lync Server. En ese caso, la prueba se realizará sin ningún tipo de interrupción para el Ken Myer real. Cuando la prueba de Ken Myer cierre sesión en el sistema, Ken Myer (la persona) permanecerá conectado.

Agregar el parámetro Verbose le permitirá obtener una cuenta detallada de las acciones realizadas por el cmdlet **Test-CsRegistration** para finalizar su prueba.

Quién puede iniciar este cmdlet: para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsRegistration"}

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
<td><p>Nombre de dominio completo (FQDN) del grupo que se va a probar.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto de credencial de usuario de la cuenta de usuario que se someterá a prueba. El valor enviado a UserCredential deberá ser una referencia a objeto obtenida con el cmdlet <strong>Get-Credential</strong>. Por ejemplo, este código devuelve un objeto de credencial para el usuario litwareinc\kenmyer y almacena ese objeto en una variable denominada:</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Debe facilitar la contraseña de usuario al iniciar este comando. Este parámetro no es obligatorio si inicia la prueba con las opciones configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación usada en la prueba. Los valores permitidos son:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error no graves que se pueden producir al iniciar el comando.</p></td>
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
<p>No anteponga un carácter $ al especificar los nombres de variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>Puerto SIP usado por el servicio de registrador. Este parámetro no es obligatorio si el registrador usa el puerto predeterminado 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección SIP de la cuenta de usuario que se probará, por ejemplo: -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. El parámetro UserSipAddress debe hacer referencia a la misma cuenta de usuario que UserCredential. Este parámetro no es obligatorio si inicia la prueba con las opciones configuración de supervisión de mantenimiento del grupo.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Test-CsRegistration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Test-CsRegistration** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

