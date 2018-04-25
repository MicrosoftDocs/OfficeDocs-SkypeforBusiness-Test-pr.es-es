---
title: Request-CsCertificate
TOCTitle: Request-CsCertificate
ms:assetid: 24e8ba6f-6023-4c03-a594-5b40784fd16a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425723(v=OCS.15)
ms:contentKeyID: 48274688
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Request-CsCertificate

 

_**Última modificación del tema:** 2015-03-09_

Es un modo de solicitar certificados para uso con servidores que ejecutan Lync Server y funciones de servidor. También ofrece un modo de comprobar el estado de las solicitudes de certificado existentes y, de ser necesario, de cancelar alguna de esas solicitudes (o todas). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Request-CsCertificate -New <SwitchParameter> -Type <CertType[]> [-AllSipDomain <SwitchParameter>] [-CA <String>] [-CaAccount <String>] [-CaPassword <String>] [-City <String>] [-ClientEKU <$true | $false>] [-ComputerFqdn <Fqdn>] [-Country <String>] [-DomainName <String>] [-FriendlyName <String>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-KeyAlg <RSA | ECDH_P256 | ECDH_P384 | ECDH_P521>] [-KeySize <Int32>] [-Organization <String>] [-OU <String>] [-Output <String>] [-PrivateKeyExportable <$true | $false>] [-State <String>] [-Template <String>] <COMMON PARAMETERS>

    Request-CsCertificate -List <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Retrieve <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Clear <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 crea una nueva solicitud de certificado: se comunica con la entidad de certificación atl-ca-001.litwareinc.com\\myca y solicita un nuevo certificado de WebServicesExternal.

    Request-CsCertificate -New -Type WebServicesExternal -CA "atl-ca-001.litwareinc.com\myca"

## EJEMPLO 2

En el ejemplo 2 se genera una lista con todas las solicitudes de certificado pendientes que se realizaron con el cmdlet **Request-CsCertificate**.

    Request-CsCertificate -List

## EJEMPLO 3

El Ejemplo 3 usa el parámetro Output para crear una solicitud de certificado sin conexión.

    Request-CsCertificate -New -Type WebServicesExternal -Output C:\Certificates\WebServicesExternal.cer

## EJEMPLO 4

El ejemplo 4 es un ejemplo más detallado (y más realista) de cómo usar el cmdlet Request-CsCertificate. En este ejemplo, se solicita un certificado para usarlo con Lync Server Standard Edition.

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Standard Edition Certficate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-cs-001.litwareinc.com,atl-ext.litwareinc.com"

## EJEMPLO 5

En el ejemplo 5, se solicita un certificado grupal para usar con Enterprise Edition de Lync Server

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Enterprise Edition Pool Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "pool1.litwareinc.com,pool1int.litwareinc.com,pool1ext.litwareinc.com"

## EJEMPLO 6

En el ejemplo 6 se muestra cómo puede solicitar un certificado para el Servidor perimetral interno.

    Request-CsCertificate -New -Type Internal -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Internal Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com, ap.litwareinc.com"

## EJEMPLO 7

El Ejemplo 7 es una variante del comando que se muestra en el ejemplo 6. Sin embargo, en este caso, la solicitud se realiza para el Servidor perimetral externo.

    Request-CsCertificate -New -Type AccessEdgeExternal,DataEdgeExternal,AudioVideoAuthentication -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "External Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com,ap.litwareinc.com,dp.litwareinc.com,atl-edge-001"

## Descripción detallada

Lync Server usa certificados para hacer que los servidores y los roles de servidor puedan comprobar sus identidades; por ejemplo, el Servidor perimetral usa certificados para comprobar que el equipo con el que se está comunicando realmente sea un Servidor front-end y viceversa. Para implementar Lync Server completamente, deberá tener los certificados correctos asignados a los roles de servidor correspondientes.

Un modo de solicitar certificados para usarlos con Lync Server es llamando al cmdlet **Request-CsCertificate**. Si bien es posible usar otras herramientas estándar de Windows a fin de solicitar certificados para usarlos con Lync Server, una ventaja importante de usar el cmdlet **Request-CsCertificate** es que este analizará la topología antes de ponerse en contacto con la entidad de certificación (CA). Sobre la base de dicho análisis, el cmdlet **Request-CsCertificate** automáticamente solicitará un certificado con los campos correspondientes de nombre de sujeto y nombre alternativo de sujeto.

El cmdlet **Request-CsCertificate** se ha diseñado para solicitar certificados que específicamente se usarán con Lync Server. No se ha diseñado como una herramienta de administración de certificados para todo propósito.

Además de solicitar certificados nuevos, este cmdlet también puede revisar las solicitudes de certificado pendientes, siempre que se hayan realizado con el cmdlet **Request-CsCertificate**. El cmdlet **Request-CsCertificate** también sirve para eliminar solicitudes de certificado pendientes, siempre y cuando se hayan realizado con el cmdlet.

Cuando intente recuperar solicitudes de certificado, posiblemente reciba un mensaje de error si tiene solicitudes revocadas. Actualmente, el cmdlet **Request-CsCertificate** solo es compatible con estos tipos de solicitudes: Emitida, Denegada y Pendiente. Si tiene problemas debido a un certificado revocado, use un comando similar al siguiente para borrar la solicitud revocada (donde 224 es el RequestID de la solicitud de certificado revocada):

Request-CsCertificate –Clear –RequestID 224

A continuación, debería poder recuperar las solicitudes de certificados.

Quiénes pueden ejecutar este cmdlet: Debe ser administrador local y tener derechos con la autoridad de certificación especificada a fin de ejecutar el cmdlet **Request-CsCertificate** en forma local. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Request-CsCertificate"}

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
<td><p><em>Clear</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, elimina las solicitudes de certificado pendientes realizadas con el cmdlet <strong>Request-CsCertificate</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>List</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, genera una lista de las solicitudes de certificado pendientes realizadas con el cmdlet <strong>Request-CsCertificate</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>New</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, indica que se desea solicitar un certificado nuevo.</p></td>
</tr>
<tr class="even">
<td><p><em>Retrieve</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, recupera las solicitudes de certificado pendientes realizadas con el cmdlet <strong>Request-CsCertificate</strong> e intenta completar la operación e importar el certificado solicitado.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo de certificado solicitado. Entre los tipos de certificados se encuentran:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (solo Microsoft Lync Online 2010)</p>
<p>ProvisionService (solo Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Por ejemplo, en esta sintaxis se solicita un nuevo certificado predeterminado: -Type Default.</p>
<p>Puede especificar varios tipos en un único comando al separar los tipos de certificados con comas:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>AllSipDomain</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando está presente, todos los dominios SIP se agregan automáticamente al campo Nombre alternativo de sujeto de los certificados. Si no está presente, solo se agrega el dominio SIP principal de forma predeterminada. Sin embargo, se pueden especificar dominios adicionales con el parámetro DomainName.</p></td>
</tr>
<tr class="odd">
<td><p><em>CA</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de dominio completo (FQDN) que señala a la entidad de certificación. Por ejemplo: -CA &quot;atl-ca-001.litwareinc.com\myca&quot;. Para obtener una lista de CA conocidas, escriba el siguiente texto en el aviso de Windows PowerShell y, luego, presione ENTER:</p>
<p>certutil</p>
<p>La propiedad Config que devuelve Certutil indica la ubicación de una CA.</p></td>
</tr>
<tr class="even">
<td><p><em>CaAccount</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de cuenta del usuario que solicita el nuevo certificado, con el formato nombre_de_dominio\nombre_de_usuario. Por ejemplo: -CaAccount &quot;litwareinc\kenmyer&quot;. Si no se especifica, el cmdlet <strong>Request-CsCertificate</strong> solicitará el nuevo certificado con las credenciales del usuario cuya sesión esté iniciada.</p></td>
</tr>
<tr class="odd">
<td><p><em>CaPassword</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Contraseña del usuario que solicita el certificado nuevo (según se especifica con el parámetro CaAccount).</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Ciudad donde se implementará el certificado.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientEKU</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Defina este parámetro en True si el certificado se usará para la autenticación de clientes. Este tipo de autenticación es obligatoria si desea que los usuarios puedan intercambiar mensajes instantáneos con personas que tienen cuentas de AOL. La parte EKU del nombre del parámetro es la abreviación de &quot;uso mejorado de clave&quot;; el campo de uso mejorado de clave enumera los usos válidos del certificado.</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del equipo para el cual se solicita el certificado. Cuando está presente, este parámetro fuerza al cmdlet <strong>Request-CsCertificate</strong> a conectarse con Almacén de administración central a fin de ubicar el equipo especificado. Siempre debe usar el nombre del equipo al solicitar un certificado, incluso cuando solicita un certificado grupal. El cmdlet <strong>Request-CsCertificate</strong> agregará automáticamente el nombre del grupo al nombre de sujeto de cualquier certificado obtenido mediante este cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>País o región donde se implementará el certificado.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainName</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Lista separada por comas de los nombres de dominio completos que se deberían agregar al campo de Nombre alternativo de sujeto del certificado. Por ejemplo:</p>
<p>-DomainName &quot;atl-cs-001.litwareinc.com, atl-cs-002.litwareinc.com,atl-cs-003.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan producirse al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>FriendlyName</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre asignado por el usuario que permite identificar el certificado más fácilmente.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN de un servidor de catálogo global en su dominio. Este parámetro no es obligatorio si ejecuta el cmdlet <strong>Request-CsCertificate</strong> en un equipo con una cuenta de su dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo de un controlador de dominio donde se almacena la configuración global. Si la configuración global está almacenada en el contenedor del sistema de Servicios de dominio de Active Directory, este parámetro debe apuntar al controlador del dominio raíz. Si la configuración global se almacena en el contenedor de configuración, es posible usar cualquier controlador de dominio y este parámetro puede omitirse.</p></td>
</tr>
<tr class="even">
<td><p><em>KeyAlg</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.X509Certificates.KeyAlgorithmIdentifier</p></td>
<td><p>Indica el tipo de algoritmo criptográfico que se usará para generar las claves pública y privada de un certificado nuevo. Entre los algoritmos de clave válidos se encuentran:</p>
<p>RSA</p>
<p>ECDH_P256</p>
<p>ECDH_P384</p>
<p>ECDH_P521</p></td>
</tr>
<tr class="odd">
<td><p><em>KeySize</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Int32</p></td>
<td><p>Indica el tamaño (en bits) de la clave privada usada por el certificado. Las claves de mayor tamaño son más seguras, pero requieren mayor sobrecarga de procesamiento a fin de descifrarla.</p>
<p>Los tamaños de claves válidos son 1024; 2048; y 4096. Por ejemplo: -KeySize 2048.</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de la organización que solicita el nuevo certificado. Por ejemplo: -Organization &quot;Litwareinc&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Unidad organizativa de Active Directory del equipo al que se asignará el nuevo certificado.</p></td>
</tr>
<tr class="even">
<td><p><em>Output</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Ruta de acceso al archivo del certificado. Si desea generar una solicitud de certificado sin conexión, use el parámetro Output y especifique la ruta de acceso del archivo de la solicitud del certificado, por ejemplo: -Output C:\Certificates\NewCertificate.pfx. De esta manera se generará un archivo de solicitud de certificado que se puede enviar por correo a una entidad de certificación para su procesamiento.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Defina este parámetro en True si desea que la clave privada del certificado se vuelva exportable. Cuando una clave privada es exportable, el certificado puede copiarse y usarse en varios equipos.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Le permite especificar una ruta de acceso para el archivo de registro creado cuando se ejecuta el cmdlet. Por ejemplo: -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestId</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Int32</p></td>
<td><p>Número de identificación asociado a una solicitud de certificado. El parámetro RequestID es un modo de asignar a una lista, recuperar o borrar un certificado individual.</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Estado de EE. UU. donde se implementará el certificado. Por ejemplo: -State WA.</p></td>
</tr>
<tr class="odd">
<td><p><em>Template</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Indica la plantilla de certificado que se usará para generar el certificado nuevo; por ejemplo: -Template &quot;WebServer&quot;. La plantilla solicitada debe estar instalada en la CA. Tenga en cuenta que el valor especificado debe ser el nombre de la plantilla, no el nombre para mostrar de la plantilla.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Request-CsCertificate** no acepta entradas canalizadas.

## Tipos de valores devueltos

Ninguno. En cambio, el cmdlet **Request-CsCertificate** ayuda a administrar instancias del objeto Microsoft.Rtc.Management.Deployment.CertificateReference.

## Vea también

#### Otros recursos

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

