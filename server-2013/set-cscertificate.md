---
title: Set-CsCertificate
TOCTitle: Set-CsCertificate
ms:assetid: 6da0be05-b257-4258-9d6d-7ddf283f1038
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398518(v=OCS.15)
ms:contentKeyID: 48275629
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCertificate

 

_**Última modificación del tema:** 2015-03-09_

Le permite asignar un certificado a un servidor o un rol de servidor de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsCertificate -Reference <CertificateReference> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCertificate -Identity <XdsIdentity> -Path <String> -Type <CertType[]> [-Password <String>] <COMMON PARAMETERS>

    Set-CsCertificate -Thumbprint <String> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1, asigna el certificado con la huella digital Thumbprint B142918E463981A76503828BB1278391B716280987B al rol de WebServicesExternal en el equipo local.

    Set-CsCertificate -Type WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## EJEMPLO 2

En el ejemplo 2 se asigna el certificado con la huella digital B142918E463981A76503828BB1278391B716280987B a tres roles diferentes en el equipo local: Predeterminado, WebServicesInternal y WebServicesExternal.

    Set-CsCertificate -Type Default, WebServicesInternal, WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## Descripción detallada

Lync Server usa certificados para hacer que los servidores y los roles de servidor puedan comprobar sus identidades; por ejemplo, el Servidor perimetral usa certificados para comprobar que el equipo con el que se está comunicando realmente sea un Servidor front-end y viceversa. Para implementar Lync Server completamente, deberá tener los certificados correctos asignados a los roles de servidor correspondientes.

El cmdlet **Set-CsCertificate** permite que los administradores asignen un certificado a un servidor o a un rol de servidor. Observe que solo puede asignar certificados que ya se han configurado para ser usados con Lync Server. Para identificar certificados disponibles para asignación, use el cmdlet **Get-CsCertificate**.

Quiénes pueden ejecutar este cmdlet: Debe ser administrador local para ejecutar el cmdlet **Set-CsCertificate** localmente. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCertificate"}

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
<td><p>Cuando se establece en Global, habilita el certificado para que funcione en el ámbito global. Los certificados globales se copiarán y distribuirán automáticamente en los equipos adecuados.</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ruta de acceso completa al archivo de certificado .PFX.</p></td>
</tr>
<tr class="odd">
<td><p><em>Reference</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertificateReference</p></td>
<td><p>Objeto que hace referencia a un certificado configurado para ser usado con Lync Server. El comando siguiente devuelve una referencia a objeto (la variable $x) que representa un certificado con la huella digital B142918E463981A76503828BB1278391B716280987B:</p>
<p>$x = Get-CsCertificate | Where-Object {$_.Thumbprint –eq &quot;B142918E463981A76503828BB1278391B716280987B&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificador único para el certificado. La huella digital de un certificado se parece a esto: B142918E463981A76503828BB1278391B716280987B.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo de certificado asignado. Entre los tipos de certificados se incluyen, sin limitaciones, los siguientes:</p>
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
<p>Por ejemplo, esta sintaxis asigna el certificado Default: -Type Default.</p>
<p>Puede especificar varios tipos en un único comando al separar los tipos de certificados con comas:</p>
<p>-Type Internal,External,Default</p></td>
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
<td><p>Fecha y hora en que se usó el certificado por primera vez. Por ejemplo, para configurar un certificado para que se use por primera vez a las 8:00 del 31/07/2012, use esta sintaxis en un servidor que se ejecute con una configuración regional Inglés (Estados Unidos):</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita que se muestre cualquier mensaje de error no grave que pueda surgir cuando se ejecuta el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Contraseña del certificado.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite registrar información detallada sobre los procedimientos llevados a cabo por el cmdlet <strong>Set-CsCertificate</strong>. El valor de parámetro debe ser la ruta completa al archivo HTML que se debe generar; por ejemplo: -Report C:\Registros\Certificates.html. Si el archivo especificado ya existe, se sobrescribirá automáticamente con la nueva información.</p></td>
</tr>
<tr class="odd">
<td><p><em>Roll</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Le permite actualizar el certificado en cuestión a la fecha y hora especificadas en el parámetro EffectiveDate. Esta hora y esta fecha indican el momento en que el nuevo certificado pasará a ser el certificado principal. Tenga en cuenta que el comando dará error si especifica el parámetro Roll sin incluir el parámetro EffectiveDate.</p></td>
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

Microsoft.Rtc.Management.Deployment.CertificateReference.

## Tipos de valores devueltos

El cmdlet **Set-CsCertificate** no devuelve ningún valor ni objeto.

## Vea también

#### Otros recursos

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)

