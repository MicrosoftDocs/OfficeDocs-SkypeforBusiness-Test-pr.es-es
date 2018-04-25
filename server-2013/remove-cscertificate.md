---
title: Remove-CsCertificate
TOCTitle: Remove-CsCertificate
ms:assetid: b7a83a58-9d3f-458a-867e-44466c9817dc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412895(v=OCS.15)
ms:contentKeyID: 48276461
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCertificate

 

_**Última modificación del tema:** 2015-03-09_

Quita un certificado marcado anteriormente como disponible para su uso por parte de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsCertificate -Type <CertType[]> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsIdentity>] [-Previous <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 elimina todos los certificados WebServicesExternal disponibles para Lync Server. Si alguno de estos certificados se está usando en estos momentos, el cmdlet **Remove-CsCertificate** le preguntará si está seguro de que desea quitar el certificado. Tendrá que responder a la pregunta para que se lleve a cabo el comando. Para eludir la pregunta de confirmación, utilice el parámetro Force:

Remove-CsCertificate –Type WebServicesExternal -Force

    Remove-CsCertificate -Type WebServicesExternal

## Descripción detallada

Lync Server usa certificados para hacer que los servidores y los roles de servidor puedan comprobar sus identidades; por ejemplo, un Servidor perimetral usa certificados para comprobar que el equipo con el que se están comunicando realmente sea un Servidor front-end y viceversa. Para implementar Lync Server completamente, deberá tener los certificados correctos asignados a los roles de servidor correspondientes.

El cmdlet **Remove-CsCertificate** permite quitar los certificados que actualmente usa Lync Server. El cmdlet **Remove-CsCertificate** no elimina realmente el certificado, sino que lo marca para indicar que ya no está disponible para que lo use Lync Server, quita todos los enlaces con el certificado y revoca los permisos de acceso al certificado (suponiendo que ningún otro servicio va a usar el certificado). Esto significa, por ejemplo, que el certificado no volverá a aparecer cuando se ejecute el cmdlet **Get-CsCertificate**.

Para volver a usar el certificado con Lync Server, deberá volver a asignar el certificado a Lync Server con el cmdlet **Set-CsCertificate**.

Si intenta quitar un certificado que está actualmente en uso, el cmdlet **Remove-CsCertificate** preguntará si está seguro de que desea quitarlo. El certificado no se quitará hasta que responda a la pregunta. Para eludir la pregunta y eliminar sigilosamente un certificado, incluso aunque esté en uso, agregue el parámetro Force al comando:

Remove-CsCertificate –Type WebServicesExternal -Force

Quién puede iniciar este cmdlet: para iniciar el cmdlet **Remove-CsCertificate** localmente, es necesario ser administrador local y miembro del dominio. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCertificate"}

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
<td><p><em>Type</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo de certificado que se debe eliminar. Entre los tipos de certificados se incluyen, sin limitaciones:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>PICWebService (solo Microsoft Lync Online 2010)</p>
<p>ProvisionService (solo Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Por ejemplo, esta sintaxis elimina el certificado Default: -Type Default.</p>
<p>Puede eliminar varios tipos con un solo comando separando los tipos de certificado con comas:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elude la pregunta de confirmación que suele presentarse cuando se intenta eliminar un certificado que está actualmente en uso.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Cuando se establece en Global, quita el certificado del ámbito global. Cuando no se especifica, los certificados se quitan del equipo local.</p></td>
</tr>
<tr class="odd">
<td><p><em>Previous</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Cuando se especifica, quita el certificado instalado anteriormente en vez del certificado asignado actualmente.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite registrar información detallada sobre los procedimientos llevados a cabo por el cmdlet <strong>Remove-CsCertificate</strong>. El valor de parámetro debe ser la ruta completa al archivo HTML que se debe generar; por ejemplo: -Report C:\Registros\Certificates.html. Si el archivo especificado ya existe, se sobrescribirá automáticamente con la nueva información.</p></td>
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

Ninguno. El cmdlet Remove-CsCertificate no acepta entradas canalizadas.

## Tipos de valores devueltos

Ninguno. En lugar de eso, el cmdlet **Remove-CsCertificate** elimina las instancias del objeto Microsoft.Rtc.Management.Deployment.CertificateReference.

## Vea también

#### Otros recursos

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

