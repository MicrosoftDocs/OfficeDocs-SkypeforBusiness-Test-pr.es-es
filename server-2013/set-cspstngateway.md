---
title: Set-CsPstnGateway
TOCTitle: Set-CsPstnGateway
ms:assetid: 5d61e7e5-dacb-4dd3-bdd5-b757d98181d3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398408(v=OCS.15)
ms:contentKeyID: 48275404
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnGateway

 

_**Última modificación del tema:** 2015-03-09_

Modifica las propiedades de la puerta de enlace de una red telefónica conmutada (RTC). Las puertas de enlace RTC ayudan a redirigir las llamadas entre los dispositivos en la red externa RTC y los dispositivos en la red interna de telefonía IP empresarial. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsPstnGateway [-Identity <XdsGlobalRelativeIdentity>] [-AlternateByPassId <String>] [-Confirm [<SwitchParameter>]] [-Default <$true | $false>] [-Force <SwitchParameter>] [-GatewaySipClientTcpPort <UInt16>] [-GatewaySipClientTlsPort <UInt16>] [-MediationServer <String>] [-RepresentativeMediaIP <String>] [-Routable <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 configura la puerta de enlace PstnGateway:192.168.0.240 como la puerta de enlace predeterminada. Significa que PstnGateway:192.168.0.240 se puede usar para administrar llamadas provenientes de Office Communications Server 2007 R2.

    Set-CsPstnGateway -Identity "PstnGateway:192.168.0.240" -Default $True

## EJEMPLO 2

En el ejemplo 2 se configuran todas las puertas de enlace RTC de la organización para garantizar que todas ellas pueden usarse en el enrutamiento saliente. En primer lugar, el comando usa el cmdlet **Get-CsService** y el parámetro PstnGateway para devolver una colección con todas las puertas de enlace RTC que actualmente se encuentran en uso. A continuación, esta colección se canaliza al cmdlet **ForEach-Object**. El cmdlet **ForEach-Object** ejecuta el cmdlet **Set-CsPstnGateway** con las distintas puertas de enlace de la colección. La propiedad Routable se establece en True para todas las puertas de enlace.

    Get-CsService -PstnGateway | ForEach-Object {Set-CsPstnGateway -Identity $_.Identity -Routable $True}

## Descripción detallada

Las puertas de enlace RTC habilitan a los usuarios de Telefonía IP empresarial a realizar y recibir llamadas de teléfono de personas en la red RTC. Estas puertas de enlace actúan como puente entre la Servidor de mediación y la red RTC.

Las puertas de enlace RTC generalmente son necesarias cuando se está usando un sistema telefónico de central pública de conmutación (PBX) con múltiplex por división de tiempo. En ese caso, generalmente, se debe emplear la puerta de enlace RTC y un servidor de mediación para enrutar las llamadas de Telefonía IP empresarial hacia la red RTC. Por el contrario, si usa un sistema IP-PBX, puede crear una conexión SIP directa entre la PBX y la Servidor de mediación, con lo cual ya no se necesita una puerta de enlace de RTC.

Una vez Instaladas y configuradas, las puertas de enlace RTC se pueden administrar mediante el uso del cmdlet **Set-CsPstnGateway**

Quiénes pueden ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsPstnGateway** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles personalizados RBAC que haya creado usted), ejecute el siguiente comando en el aviso de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnGateway"}

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
<td><p><em>AlternateByPassId</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Identificador único global (GUID) que representa el identificador de desvío alternativa. Este identificador se genera automáticamente mediante Lync Server y se usa para ayudar a eliminar las llamadas &quot;hairpin&quot;. Según se haya configurado el sistema, las llamadas 'hairpin' pueden desviar automáticamente el Servidor de mediación sin que usted deba definir y asociar subredes individuales a todos los sitios y regiones.</p>
<p>Para eso, generalmente se necesita habilitar la desviación globalmente para usar sitios y regiones de configuración de red, y habilitar la desviación en la configuración troncal de la puerta de enlace RTC.</p>
<p>La llamada hairpin se produce cuando se vuelve a enrutar una llamada entrante desde la red RTC a esa red a través del desvío de llamadas o llamadas simultáneas.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Default</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si se establece en True, esta puerta de enlace administrará llamadas desde Office Communications Server 2007 R2. Solo puede haber una puerta de enlace predeterminada en la recopilación de puertas de enlace administradas por un único Servidor de mediación.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime cualquier aviso de confirmación o mensaje de error leve que se pueda producir al ejecutar el cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>GatewaySipClientTcpPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto de escucha usado para comunicarse con servidores de mediación mediante el uso del Protocolo de control de transmisión (TCP). El valor predeterminado es 5066.</p></td>
</tr>
<tr class="even">
<td><p><em>GatewaySipClientTlsPort</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Puerto de escucha usado para comunicarse con servidores de mediación mediante el uso del protocolo de seguridad de la capa de transporte (TLS). El valor predeterminado es 5067.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identidad de servicio de la puerta de enlace RTC que se debe modificar. Por ejemplo: -Identity &quot;PstnGateway:192.168.0.240&quot;.</p>
<p>Tenga en cuenta que puede dejar el prefijo &quot;PstnGatewayServer:&quot; al especificar una puerta de enlace de RTC. Por ejemplo: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Identidad de servicio del Servidor de mediación que se debe asociar a la puerta de enlace RTC. Por ejemplo: -MediationServer &quot;MediationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>RepresentativeMediaIP</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Dirección IP del procesador de medios asociado a la puerta de enlace, siempre que la ubicación del procesador sea distinta a la dirección de señalización. Tanto la desviación de medios como el control de admisión de llamadas (CAC) se basan en la ubicación del procesador de medios de la puerta de enlace; de forma predeterminada, es la misma ubicación que la dirección de señalización. Si las dos ubicaciones son diferentes (por ejemplo, con el procesador de medios en un sitio remoto y el par de señalización en el sitio central), RepresentativeMediaIP debe configurarse con la dirección IP del procesador de medios.</p>
<p>Si ha implementado varios procesadores de medios en el mismo sitio, cada uno con su propia dirección IP, puede usar cualquiera de estas direcciones IP al configurar la propiedad RepresentativeMediaIP.</p></td>
</tr>
<tr class="even">
<td><p><em>Routable</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Cuando está establecida en True, la puerta de enlace se puede usar en rutas de enrutamiento de salida.</p></td>
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

Ninguno. El cmdlet **Get-CsPstnGateway** no acepta canalizaciones.

## Tipos de valores devueltos

El cmdlet **Set-CsPstnGateway** no devuelve objetos ni valores. En su lugar, el cmdlet modifica las instancias existentes del objeto Microsoft.Rtc.Management.Xds.DisplayPstnGateway.

## Vea también

#### Otros recursos

[Get-CsService](get-csservice.md)

