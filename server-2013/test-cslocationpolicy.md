---
title: Test-CsLocationPolicy
TOCTitle: Test-CsLocationPolicy
ms:assetid: 49f7d148-d46d-4bcc-af9d-6a3a0fdde8ee
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425962(v=OCS.15)
ms:contentKeyID: 48275187
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLocationPolicy

 

_**Última modificación del tema:** 2015-03-09_

Ejecuta una prueba para determinar la directiva de ubicación que se usará según los criterios especificados en los valores de parámetro. La directiva de ubicación contiene las configuraciones que determinarán si 9-1-1 mejorado (E9-1-1) se aplicará y cómo se llevará a cabo dicha implementación. E9-1-1 habilita a aquellos que responden llamadas de emergencia del 911 a determinar la ubicación geográfica del autor de la llamada. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsLocationPolicy -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Subnet <String>]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se determina la directiva de ubicación del usuario actual (o el usuario actualmente configurado). Se requiere TargetFqdn.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com 

## EJEMPLO 2

La primera línea en el ejemplo 2 es una llamada al cmdlet **Get-Credential** de Windows PowerShell. Este cmdlet recuperará las credenciales de usuario y las devolverá como un objeto seguro. El único parámetro proporcionado a este cmdlet es user ID. La ejecución de este cmdlet abrirá un cuadro de diálogo que se completará previamente con el Id. de usuario proporcionado y que posee un cuadro de texto que le permite escribir la contraseña de usuario. Estas credenciales de usuario se guardan en la variable $cred.

La línea 2 llama al cmdlet **Test-CsLocationPolicy**. Al igual que el ejemplo 1, se suministra el FQDN de destino. Sin embargo, en este ejemplo, en vez de usar un usuario preconfigurado, se ejecutará la prueba en función del usuario con la dirección SIP kenmyer@litwareinc.com. Ese valor se transfiere (con el sip: prefijo) al parámetro UserSipAddress y las credenciales para ese usuario (almacenadas en la variable $cred) al parámetro UserCredential.

    $cred = Get-Credential "litwareinc\kenmyer"
    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred -UserSipAddress "sip:kenmyer@litwareinc.com"

## EJEMPLO 3

Este ejemplo es similar al ejemplo 2, sin las credenciales de usuario especificadas. Si se llama al cmdlet **Test-CsLocationPolicy** sin especificar credenciales de usuario, el certificado de servidor del equipo donde se ejecuta este cmdlet se usa para autenticar y detectar la directiva de ubicación del usuario. Si el equipo no cuenta con un certificado de servidor, deben especificarse las credenciales, como se muestra en el ejemplo 2. Para descubrir si el equipo dispone de certificado de servidor, llame al cmdlet **Get-CsCertificate**.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com"

## EJEMPLO 4

En este ejemplo, se determina la directiva de ubicación de la subred con el Id. de subred 172.15.11.0. Si la subred no está asociada con una directiva de ubicación, se recuperará la directiva de ubicación para el usuario actualmente configurado.

Nota: Una directiva de ubicación se establece en una subred mediante la configuración del parámetro LocationPolicy del cmdlet **Set-CsNetworkSite** en el Id. de la directiva de ubicación y, luego, mediante la configuración del parámetro NetworkSiteId del cmdlet **Set-CsNetworkSubnet** en el Id. de ese sitio. Por ejemplo:

Set-CsNetworkSite Portland –LocationPolicy Reno

Set-CsNetworkSubnet 175.15.11.0 –NetworkSiteID Portland

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -Subnet 172.15.11.0

## Descripción detallada

La directiva de ubicación se usa para aplicar configuraciones que se relacionan con la funcionalidad de E9-1-1 y la ubicación del cliente. La directiva de ubicación determina si un usuario está habilitado para E9-1-1 y, si es así, cuál es el comportamiento de una llamada de emergencia. Por ejemplo, puede usar la directiva de ubicación para definir qué número constituye una llamada de emergencia (911 en los EE. UU.), si se debe informar a la seguridad corporativa de forma automática y cómo se debe desviar la llamada. Este cmdlet devuelve información acerca de la directiva de ubicación que se usará cuando se realizan llamadas desde un cliente en particular en un grupo, subred, conmutador o punto de acceso inalámbrico específico.

Si no se especifica un usuario al llamar a este cmdlet, se probará el usuario que se encuentra configurado actualmente. Para buscar este usuario, llame al cmdlet **Get-CsHealthMonitoringConfiguration**. Para establecer el usuario configurado, llame al cmdlet **Set-CsHealthMonitoringConfiguration**.

Si se encontró una directiva de ubicación para el usuario o la subred, la prueba será correcta. La información devuelta de forma predeterminada incluye el nombre de la directiva de ubicación (en caso de que se asigne una directiva por usuario) y si el usuario o la subred están habilitados para E9-1-1. Incluye el parámetro común Verbose de Windows PowerShell para recuperar información adicional acerca de la prueba.

Puede probar directivas de ubicación en usuarios o subredes. Si ejecuta la prueba en una subred (mediante la especificación de un valor para el parámetro Subnet), el cmdlet intentará resolver la directiva de ubicación para esa subred. Si no se asigna ninguna directiva de ubicación a la subred, se recuperará la directiva de ubicación para el usuario configurado. Si la directiva de subred se recupera correctamente, la salida incluirá un valor LocationPolicyTagID que se iniciará con el Id. de etiqueta de la subred. Si no se encontró una directiva de ubicación para la subred, LocationPolicyTagID comenzará con el Id. de etiqueta del usuario.

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos están autorizados a ejecutar el cmdlet **Test-CsLocationPolicy** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLocationPolicy"}

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
<td><p>El nombre de dominio completo (FQDN) del grupo en el que se hospeda el usuario o la subred específica. (Si no se especifica un usuario, el usuario actual o preconfigurado se da por supuesto).</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Un objeto que contiene el identificador de usuario y la contraseña de la cuenta de usuario en la que se está probando la directiva de ubicación. Para recuperar un objeto de credenciales, llame al cmdlet <strong>Get-Credential</strong>, rellene la información correspondiente y guarde el resultado en una variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación usado en la prueba. Los valores permitidos son:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las solicitudes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Cuando esté presente, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Por ejemplo, para almacenar resultados en una variable llamada $TestOutput, utilice la sintaxis siguiente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>No anteponga un carácter $ al especificar el nombre de variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>El número de puerto del servicio registrador.</p></td>
</tr>
<tr class="even">
<td><p><em>Subnet</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>El Id. (la dirección IP) de la subred para la cual desea probar la directiva de ubicación.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>La dirección SIP del usuario cuya directiva de ubicación se desea probar. Esta se debe estar con el formato sip:&lt;Id. de usuario&gt;, por ejemplo, sip:kenmyer@litwareinc.com.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Test-CsLocationPolicy** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

