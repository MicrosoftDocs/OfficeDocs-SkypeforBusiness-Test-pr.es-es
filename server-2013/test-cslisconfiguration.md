---
title: Test-CsLisConfiguration
TOCTitle: Test-CsLisConfiguration
ms:assetid: 6983d42e-6b93-4365-b0f1-81031d6e251b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398497(v=OCS.15)
ms:contentKeyID: 48275543
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Prueba la configuración del servidor de información de ubicación (LIS). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Test-CsLisConfiguration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BssId <String>] [-ChassisId <String>] [-Force <SwitchParameter>] [-Mac <String>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PortId <String>] [-PortIdSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-Subnet <String>]

## Ejemplos

## EJEMPLO 1

En este ejemplo se prueba la configuración del LIS en el nombre de dominio completo atl-cs-001.litwareinc.com. La prueba se considerará superada si se puede establecer una conexión con las credenciales de usuario actuales y el servicio web del LIS en ese nombre de dominio completo. Si se encuentra alguna ubicación asignada a la dirección IP 192.168.0.0 de la subred, se devolverá la dirección de esa ubicación.

Para que este comando se ejecute correctamente, debe haber una configuración de supervisión de mantenimiento que contenga usuarios de transacción sintética. Para saber si existe una configuración de supervisión de mantenimiento, ejecute el cmdlet **Get-CsHealthMonitoringConfiguration**. Para crear una configuración de supervisión de mantenimiento nueva, ejecute el cmdlet **New-CsHealthMonitoringConfiguration**.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0

## EJEMPLO 2

Este ejemplo es idéntico al ejemplo 1, si bien se integra el parámetro UserSipAddress. Use este comando cuando no se hayan configurado usuarios de transacción sintética y el equipo en el que el comando se ejecuta carece de un certificado de servidor.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com

## EJEMPLO 3

La primera línea de este ejemplo llama a un cmdlet de Windows PowerShell, el cmdlet **Get-Credential**, que solicita al usuario un identificador de usuario y una contraseña. Esta información se almacena de forma cifrada en la variable $cred.

La segunda línea es idéntica al comando del ejemplo 2, si bien se integra el parámetro UserSipAddress. Use este comando cuando no se hayan configurado usuarios de transacción sintética y el equipo en el que el comando se ejecuta carece de un certificado de servidor.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com -UserCredential $cred

## EJEMPLO 4

La primera línea de este ejemplo llama al cmdlet **Get-Credential**, que solicita al usuario un identificador de usuario y una contraseña. Esta información se almacena de forma cifrada en la variable $cred.

La línea 2 llama al URI del servicio web para probar la configuración del LIS (https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc) a partir de la dirección SIP del usuario remoto (sip:kmyer@litwareinc.com), y usa las credenciales que obtuvimos en la línea 1 pasándolas al parámetro WebCredential. La prueba se considerará superada si se puede establecer una conexión con las credenciales de usuario facilitadas y el servicio web del LIS en ese URI. Si se encuentra alguna ubicación asignada a la dirección IP de subred 192.168.0.0, la dirección MAC 0A-23-00-00-00-AA o el Id. de puerto 4500 y ChassisId 0A-23-00-00-00-AA, se devolverá la dirección de esa ubicación.

Use este comando cuando el equipo en el que el comando se ejecuta carece de un certificado de servidor.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -WebCredential $cred -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## EJEMPLO 5

Este ejemplo es idéntico al ejemplo 4, excepto por el hecho de que el comando no usa el parámetro WebCredential (y, por lo tanto, no llama al cmdlet **Get-Credential**). Use este comando cuando el PC en el que se inicia el comando tiene un certificado de servidor.

    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## Descripción detallada

Este cmdlet determina si se puede establecer contacto con el servicio web del servidor de información de ubicaciones (LIS) en función de la información de los parámetros facilitados. Si se puede contactar con el servicio web y se encuentra una ubicación que corresponda a cualquiera de los parámetros facilitados, se considerará superada la prueba y se mostrará la ubicación. Si, aun cuando no se encuentre la ubicación, se puede establecer contacto con el servicio web, la prueba se realizará correctamente, aunque sin información de ubicación. Además, si llama a este cmdlet sin facilitar ningún parámetro opcional, la prueba se considerará superada si se puede establecer contacto con el servicio, aunque, de nuevo, no se devolverá ninguna información de ubicación.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Test-CsLisConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsConfiguration"}

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
<td><p>El nombre de dominio completo, FQDN (con la forma server.litwareinc.com) del servidor en el que desea ejecutar la prueba.</p>
<p>Este parámetro es obligatorio a menos que especifique el parámetro TargetUri, en cuyo caso no podrá especificar TargetFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Cadena</p></td>
<td><p>Identificador uniforme de recursos (URI) del Servicio de información de ubicaciones. Puede recuperar el URI del Servicio de información de ubicaciones ejecutando el siguiente comando: Get-CsService –WebServer | Select-Object LIServiceInternalUri</p>
<p>Si especifica un valor para este parámetro, se necesita también el parámetro UserSipAddress. Si el equipo donde se ejecuta el comando carece de un certificado de servidor, también tendrá que especificar un valor en el parámetro WebCredential.</p>
<p>Este parámetro es obligatorio si no especifica el parámetro TargetFqdn.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto que contiene credenciales de usuario para obtener acceso al Servicio de información de ubicaciones. Este objeto se puede recuperar llamando al <strong>Get-Credential</strong> y facilitando las credenciales correspondientes.</p>
<p>Este parámetro es necesario si se han especificado los parámetros TargetFqdn y UserSipAddress y si el equipo en el que el cmdlet se ejecuta carece de un certificado de servidor.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Opcional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo de autenticación usado en la prueba. Los valores permitidos son::</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>BssId</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Identificador del conjunto de servicios básicos (BSSID) de un punto de acceso inalámbrico. Este valor debe estar en la forma nn-nn-nn-nn-nn-nn, por ejemplo, 12-34-56-78-90-ab.</p></td>
</tr>
<tr class="even">
<td><p><em>ChassisId</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección de Media Access Control (MAC) de un conmutador de red. Este valor debe estar en la forma nn-nn-nn-nn-nn-nn, por ejemplo, 12-34-56-78-90-ab, o como dirección IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Este parámetro no es compatible con el servidor de información de ubicaciones.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mac</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La dirección MAC del conmutador de puertos. Este valor debe estar en la forma nn-nn-nn-nn-nn-nn, por ejemplo, 12-34-56-78-90-ab.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
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
<td><p>Cadena</p></td>
<td><p>Cuando esté presente, el resultado detallado de ejecutar el cmdlet se almacenará en la variable especificada. Por ejemplo, para almacenar resultados en una variable llamada $TestOutput, utilice la sintaxis siguiente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>No anteponga un carácter $ al especificar el nombre de variable.</p></td>
</tr>
<tr class="even">
<td><p><em>PortId</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>El identificador del puerto asociado a la ubicación que se probará. También puede contener una dirección MAC o una dirección IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIdSubType</em></p></td>
<td><p>Opcional</p></td>
<td><p>PortIDSubType</p></td>
<td><p>Subtipo del puerto. Este valor se puede especificar en forma de valor numérico o de cadena de caracteres, pero debe ser un subtipo válido. Los subtipos válidos son:</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int32</p></td>
<td><p>El número de puerto del servicio registrador.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnet</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>La dirección IP de una subred. Este valor debe escribirse como dirección IPv4 (con los dígitos separados por puntos, como en 192.0.2.0).</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Dirección IP de un usuario remoto.</p>
<p>Si especifica un valor para este parámetro, los parámetros TargetFqdn o TargetUri también serán necesarios.</p>
<p>Este parámetro es necesario cuando se especifica el parámetro TargetFqdn únicamente si no se han configurado usuarios de transacción sintética. Para saber si se han configurado usuarios de transacción sintética, ejecute el cmdlet <strong>Get-CsHealthMonitoringConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSCredential</p></td>
<td><p>Objeto que contiene credenciales de usuario para obtener acceso al Servicio de información de ubicaciones. Este objeto se puede recuperar llamando al cmdlet <strong>Get-Credential</strong> y facilitando las credenciales correspondientes.</p>
<p>Este parámetro es necesario si se han especificado los parámetros TargetUri y UserSipAddress y si el equipo en el que el comando se ejecuta carece de un certificado de servidor.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

El cmdlet **Test-CsLisConfiguration** devuelve una instancia del objeto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vea también

#### Otros recursos

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)

