---
title: Get-CsVoicemailReroutingConfiguration
TOCTitle: Get-CsVoicemailReroutingConfiguration
ms:assetid: 25e401eb-6a84-468f-b0eb-5b794f20b5bc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425732(v=OCS.15)
ms:contentKeyID: 48274720
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicemailReroutingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Recupera configuraciones que proporcionan números de teléfono de la red telefónica conmutada (RTC) para obtener acceso a las características de acceso de suscriptor y operador automático de Mensajería unificada de Exchange. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicemailReroutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Ejemplos

## EJEMPLO 1

En este ejemplo, se recuperan todas las configuraciones usadas para volver a enrutar el correo de voz que se han definido en esta implementación de Lync Server. Por ejemplo, si hay tres sucursales en las que se implementa la aplicación de sucursal con funciones de supervivencia, el comando devolverá tres conjuntos de configuraciones usadas para volver a enrutar el correo de voz.

    Get-CsVoicemailReroutingConfiguration

## EJEMPLO 2

En este ejemplo, se recupera la configuración usada para volver a enrutar el correo de voz del sitio BranchOffice\_Portland.

    Get-CsVoicemailReroutingConfiguration -Identity site:BranchOffice_Portland

## EJEMPLO 3

En este ejemplo, se recupera la configuración usada para volver a enrutar el correo de voz de todos los sitios cuyos nombres comienzan con el valor de cadena BranchOffice (por ejemplo, BranchOffice\_Portland, BranchOffice\_Sacramento).

    Get-CsVoicemailReroutingConfiguration -Filter *:BranchOffice*

## EJEMPLO 4

En este ejemplo, se recuperan todas las configuraciones de nuevo enrutamiento de correo de voz que no están habilitadas. La primera parte de este comando llama al cmdlet **Get-CsVoicemailReroutingConfiguration**, el cual recupera una recopilación de todas las configuraciones de nuevo enrutamiento de correo de voz . A continuación, dicha recopilación se canaliza al cmdlet **Where-Object**. El cmdlet **Where-Object** restringe esa recopilación para incluir solo las configuraciones cuya propiedad Enabled es igual a (-eq) False.

    Get-CsVoicemailReroutingConfiguration | Where-Object {$_.Enabled -eq $False}

## Descripción detallada

Este cmdlet recupera las configuraciones que determinan hacia dónde se enrutarán las llamadas dirigidas al operador automático y al acceso de suscriptor cuando no se encuentre disponible la conectividad IP que une a Lync Server del sitio de la sucursal hasta el servidor de Mensajería unificada de Exchange ubicado en el centro de datos.

Operador automático y Acceso de suscriptor son características de Mensajería unificada de Exchange. La característica Operador automático proporciona prestaciones de reconocimiento de voz y control por tonos (tono de marcado de frecuencia múltiple o DTMF) para que los autores de llamadas externos puedan navegar por el sistema telefónico de una compañía y, así, se comuniquen con el departamento o empleado que quieran, o bien, en el modo de toma de mensajes (Message Taking), aceptar mensajes para los usuarios. (Se recomienda volver a enrutar la voz para el modo de recepción de mensajes). El acceso de suscriptor permite a los usuarios internos obtener acceso a su buzón de correo de Microsoft Outlook desde un teléfono. Los números proporcionados por esta configuración permiten a los autores de las llamadas dejar mensajes de correo de voz para los usuarios de Telefonía IP empresarial (configuración AutoAttendantNumber), así como recuperar correo de voz a dichos usuarios, aunque la conectividad IP de la implementación de Lync Server con Mensajería unificada de Exchange en un sitio remoto no esté disponible en el centro de datos (configuración SubscriberAccessNumber).

Si se llama a este cmdlet sin parámetros adicionales, se recuperarán todas las configuraciones usadas para volver a enrutar el correo de voz.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Get-CsVoicemailReroutingConfiguration** en forma local: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicemailReroutingConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>El parámetro Filter le permite recuperar la configuración de un conjunto particular de sitios, sobre la base de una coincidencia de caracteres comodín.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificador único de la configuración que se quiere recuperar. Para este cmdlet, el parámetro Identity será Global o Site:&lt;nombre del sitio&gt; (donde&lt;nombre del sitio&gt; es el nombre del sitio al cual se aplica la configuración).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la configuración del nuevo enrutamiento del correo de voz hasta la réplica local del Almacén de administración central, en lugar del propio Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Recupera uno o más objetos del tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Vea también

#### Otros recursos

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)

