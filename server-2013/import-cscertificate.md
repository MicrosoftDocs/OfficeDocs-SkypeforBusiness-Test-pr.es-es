---
title: Import-CsCertificate
TOCTitle: Import-CsCertificate
ms:assetid: 87bdafce-f4b9-4c44-ad8f-86c2deb680a4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398688(v=OCS.15)
ms:contentKeyID: 48275923
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsCertificate

 

_**Última modificación del tema:** 2015-03-09_

Importa un certificado para usarlo con Lync Server. Si un certificado no se adquiere con el cmdlet **Request-CsCertificate**, debe importarse para poder asignarse a un rol de servidor de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Import-CsCertificate -Identity <XdsIdentity> -Type <CertType[]> <COMMON PARAMETERS>

    Import-CsCertificate [-PrivateKeyExportable <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Path <String> [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Password <String>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 importa el certificado C:\\Certificates\\WebServer.pfx. Una vez que finalice el comando, el certificado estará disponible para su asignación a un rol de servidor.

    Import-CsCertificate -Path "C:\Certificates\WebServer.pfx" -PrivateKeyExportable $True

## Descripción detallada

Lync Server usa certificados para hacer que los servidores y los roles de servidor puedan comprobar sus identidades; por ejemplo, un Servidor perimetral usa certificados para comprobar que el equipo con el que se están comunicando realmente sea un Servidor front-end y viceversa. Para poder implementar completamente Lync Server, deberá tener asignados los certificados correctos a los roles del servidor correctos.

Para asignar los certificados a un rol de Lync Server, es necesario presentar dichos certificados a Lync Server. El cmdlet **Request-CsCertificate** permite pedir nuevos certificados en línea y sin conexión. Si la petición se hace en línea, el certificado se descargará automáticamente y se guardará en el almacén local de certificados; además, quedará disponible de inmediato para que lo use Lync Server. Si la petición se hace sin conexión, se envía un archivo con el certificado. En ese caso, se puede usar el cmdlet **Import-CsCertificate** para importar el certificado. Con este proceso, el certificado estará disponible para su asignación a un rol de servidor de Lync Server.

Quién puede iniciar este cmdlet: Para ejecutar el cmdlet **Import-CsCertificate** localmente, es necesario ser administrador de dominio. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsCertificate"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Si se establece en Global, permite que el certificado funcione en el ámbito global. Los certificados globales se copian y se distribuyen automáticamente a los PC adecuados.</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ruta de acceso completa del archivo del certificado que se importará. Por ejemplo: –Path &quot;C:\Certificados\WebServer.cer&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo de certificado que se pide. Entre los tipos se incluyen los siguientes:</p>
<p>* AccessEdgeExternal</p>
<p>* AudioVideoAuthentication</p>
<p>* DataEdgeExternal</p>
<p>* Default</p>
<p>* External</p>
<p>* Internal</p>
<p>* iPadAPNService</p>
<p></p>
<p>* iPhoneAPNService</p>
<p>* LogRetentionService</p>
<p>* MPNService</p>
<p>* OAuthTokenIssuer</p>
<p>* PICWebService</p>
<p>* ProvisionService</p>
<p>* SMPDNSWebService</p>
<p>* TenantAdmin</p>
<p>* UpgradeEngineService</p>
<p>* WebServicesExternal</p>
<p>* WebServicesInternal</p>
<p>* WsFedTokenTransfer</p>
<p>* XMPPServer</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EffectiveDate</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.DateTime</p></td>
<td><p>La fecha y la hora en la que puede usarse el certificado por primera vez. Por ejemplo, para configurar un certificado para usarlo por primera vez a las 8 a. m. el 31 de julio de 2012 use esta sintaxis en un servidor configurado para la región e idioma Inglés (EE. UU.):</p>
<p>-Hora efectiva &quot;31/07/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Contraseña asociada al archivo del certificado.</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Cuando tiene el valor True, comprueba que la cuenta del servicio de red puede leer la parte de la clave privada del certificado.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite especificar la ruta de acceso del archivo de registro que se crea al iniciarse el cmdlet. Por ejemplo: -Report &quot;C:\Registros\Certificados.html&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Roll</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Le permite actualizar el certificado en cuestión a la fecha y hora especificadas en el parámetro EffectiveDate. Esta hora y esta fecha indican el momento en que el nuevo certificado pasará a ser el certificado principal. Tenga en cuenta que el comando dará error si especifica el parámetro Roll sin incluir el parámetro EffectiveDate.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Import-CsCertificate** no acepta entradas canalizadas.

## Tipos de valores devueltos

Ninguno.

## Vea también

#### Otros recursos

[Get-CsCertificate](get-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

