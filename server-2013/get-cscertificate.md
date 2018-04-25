---
title: Get-CsCertificate
TOCTitle: Get-CsCertificate
ms:assetid: 15b8f019-1d00-4389-9abe-18deb8cbf2ea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398227(v=OCS.15)
ms:contentKeyID: 48274538
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCertificate

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información acerca de certificados en equipos locales que se han configurado con Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsCertificate [-Identity <XdsIdentity>] [-Report <String>] [-Type <CertType[]>]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 devuelve información acerca de los certificados que se encuentran actualmente asignados a componentes de Lync Server. Esto se lleva a cabo llamando al cmdlet **Get-CsCertificate** sin ningún parámetro adicional.

    Get-CsCertificate

## EJEMPLO 2

En el ejemplo 2 se recuperan todos los certificados de Lync Server usados para servicios web internos. Para ello, se incluye el parámetro Type, junto con el valor de parámetro WebServicesInternal.

    Get-CsCertificate -Type WebServicesInternal

## EJEMPLO 3

En el ejemplo 3 se devuelven todos los certificados de Lync Server que expiran antes del 1 de septiembre de 2012. Para llevar a cabo esta tarea, primero el comando usa el cmdlet **Get-CsCertificate** para devolver una recopilación de todos los certificados de Lync Server que se encuentran en uso actualmente. A continuación, esta recopilación se canaliza al cmdlet **Where-Object**, que selecciona solo los certificados que expiran antes del 1 de septiembre de 2012. En la fecha especificada en este ejemplo (9/1/2012) se usa el formato de inglés (Estados Unidos) para los valores de fecha y hora. Las fechas deben especificarse en un formato compatible con la configuración regional y de idioma.

    Get-CsCertificate | Where-Object {$_.NotAfter -lt "9/1/2012"}

## EJEMPLO 4

En el ejemplo 4 se devuelve información acerca de todos los certificados de Lync Server emitidos por la entidad de certificación (CA) MyCa. Para ello, el comando primero llama al cmdlet **Get-CsCertificate** sin ningún parámetro a fin de devolver una recopilación de todos los certificados que se encuentran actualmente en uso. Esta recopilación luego se canaliza al cmdlet **Where-Object**, el cual escoge todos los certificados donde la propiedad Issuer es igual a (-eq) "Cn=MyCa".

    Get-CsCertificate | Where-Object {$_.Issuer -eq "Cn=MyCa"}

## EJEMPLO 5

El comando que se muestra en el ejemplo 5 devuelve todos los certificados de Lync Server donde la propiedad Subject se ha definido en CN=atl-cs-001.litwareinc.com. Esto se lleva a cabo usando el cmdlet **Get-CsCertificate** para devolver una recopilación de todos los certificados de Lync Server y luego canalizando dicha recopilación al cmdlet **Where-Object**. A su vez, el cmdlet **Where-Object** selecciona solo aquellos certificados cuya propiedad Subject es igual a "CN=atl-cs-001.litwareinc.com".

    Get-CsCertificate | Where-Object {$_.Subject -eq "CN=atl-cs-001.litwareinc.com"}

## Descripción detallada

Lync Server usa certificados para hacer que los servidores y los roles de servidor puedan comprobar sus identidades; por ejemplo, el Servidor perimetral usa certificados para comprobar que el equipo con el que se está comunicando realmente sea un Servidor front-end y viceversa. Para implementar Lync Server completamente, necesitará tener los certificados correctos asignados a las funciones de rol correspondientes.

El cmdlet **Get-CsCertificate** ofrece un modo de recuperar información detallada acerca de los certificados que se han configurado para usarlos con Lync Server. Tenga en cuenta que el cmdlet solo devuelve información acerca de los certificados de Lync Server. Si un certificado no fue configurado para su uso con Lync Server (mediante el cmdlet **Set-CsCertificate**), no se devolverá ese certificado al ejecutar el cmdlet **Get-CsCertificate**.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Get-CsCertificate** en forma local: RTCUniversalServerAdmins.

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
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Permite recuperar certificados configurados en el ámbito global (los certificados globales se copian y se distribuyen en los equipos adecuados). Use esta sintaxis para que se devuelva información acerca de los certificados globales:</p>
<p>Get-CsCertificate –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Le permite registrar información detallada acerca de los procedimientos realizados por el cmdlet <strong>Get-CsCertificate</strong>. El valor de parámetro debe ser la ruta de acceso completa al archivo HTML que se generará, por ejemplo: -Report C:\Logs\Certificates.html. Si el archivo especificado ya existe, se sobrescribirá automáticamente con la nueva información.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo de certificado solicitado. Entre los tipos de certificados se incluyen, entre otros, los siguientes:</p>
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
<p>Por ejemplo, esta sintaxis devuelve información sobre el certificado predeterminado: -Type Default.</p>
<p>Puede especificar varios tipos en un único comando al separar los tipos de certificados con comas:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsCertificate** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsCertificate** devuelve instancias del objeto Microsoft.Rtc.Management.Deployment.CertificateReference.

## Vea también

#### Otros recursos

[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

