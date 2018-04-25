---
title: Set-CsTenantHybridConfiguration
TOCTitle: Set-CsTenantHybridConfiguration
ms:assetid: 805ac9ee-df40-40e1-baaa-adffb6bd8cf6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994046(v=OCS.15)
ms:contentKeyID: 52061663
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantHybridConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Se usa en escenarios híbridos para dar a los usuarios hospedados en Microsoft Lync Online acceso a las características de Telefonía IP empresarial local, como la omisión de medios, 9-1-1 mejorado y el estacionamiento de llamadas. Un escenario híbrido (también denominado escenario de dominio dividido) es una implementación de Lync Server en la que algunos usuarios tienen cuentas hospedadas de manera local, mientras que otros tienen cuentas hospedadas en Lync Online.

Este cmdlet solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Set-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-PeerDestination <string>] [-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]Set-CsTenantHybridConfiguration [-Tenant <guid>] [-PeerDestination <string>][-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Instance <psobject>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 establece la dirección URL del servicio interno para la colección global de opciones de configuración híbrida del inquilino. Para establecer una configuración global, incluya el parámetro Identity y el valor de parámetro "global".

    Set-CsTenantHybridConfiguration -Identity "global" - HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Ejemplo 2

En el ejemplo 2, la dirección URL del servicio interno se configura para un inquilino concreto; en este ejemplo, es el inquilino cuyo TenantID es "bf19b7db-6960-41e5-a139-2aa373474354". Cuando un valor de propiedad se asigna explícitamente a un inquilino concreto, este estará regido por las opciones de configuración híbrida del inquilino concreto en lugar de por las opciones globales de configuración.

    Set-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Ejemplo 3

El comando que se ve en el ejemplo 3 configura la dirección URL del servicio interno para todos los inquilinos de la organización. Para ello, el comando usa primero el cmdlet **Get-CsTenant** para devolver la colección de todos los inquilinos disponibles; luego, esta colección se canaliza al cmdlet **ForEach-Object**. A su vez, el cmdlet **ForEach-Object** ejecuta el cmdlet **Set-CsTenantHybridConfiguration** en cada inquilino de la colección y, así, establece la dirección URL del servicio interno de cada uno de estos inquilinos en "https://internal.litwareinc.com".

    Get-CsTenant | ForEach-Object {Set-CsTenantHybridConfiguration -Tenant $_.TenantID -HybridConfigServiceInternalUrl "https://internal.litwareinc.com"}

## Descripción detallada

En una implementación híbrida o de "dominio dividido", la organización tiene algunos usuarios con cuentas hospedadas en Lync Online a la vez que tiene otros usuarios con cuentas hospedadas en Lync Server. De manera predeterminada, los usuarios hospedados en Lync Online no tienen acceso a todas las capacidades que ofrece Telefonía IP empresarial; esto se debe a que los servidores de Lync Online no tienen acceso directo a la implementación local de Lync Server ni a la información de la configuración de red. Entre otras cosas, los usuarios de Lync Online no tienen acceso predeterminado a ciertas características:

  - 9-1-1 mejorado, el servicio de Lync Server que se usa para hacer llamadas telefónicas de emergencia.

  - Estacionamiento de llamadas, el servicio de Lync Server que permite a los usuarios poner una llamada en espera en el teléfono A y recuperar otra llamada en el teléfono B.

  - Omisión de medios, que permite que las llamadas emitidas y recibidas de la red telefónica conmutada (RTC) omitan el servidor de mediación, lo cual minimiza la transcodificación y la latencia de red.

  - Llamadas entrantes y salientes de conferencia en redes RTC, que permiten a los usuarios participar en la parte de audio de una conferencia en línea usando un teléfono de RTC o un dispositivo móvil.

  - La aplicación Grupo de respuesta, que permite redirigir automáticamente las llamadas telefónicas a entidades, como una línea de asistencia técnica o de atención al cliente. De manera predeterminada, los usuarios de Lync Online no pueden actuar como agentes del Grupo de respuesta.

Para ofrecer a los usuarios de Lync Online acceso a estas capacidades de Telefonía IP empresarial, los administradores tienen que asignar los valores apropiados a las opciones de configuración híbrida, como las dirección URL del servicio web interno, externo y el nombre de dominio completo del servidor perimetral de acceso de la organización. Estos valores, que solo se pueden configurar con el cmdlet **Set-CsTenantHybridConfiguration**, dan a los servidores de Lync Online la información necesaria para usar estas características avanzadas de Telefonía IP empresarial.

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
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p></p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan surgir al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HybridConfigServiceExternalUrl</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Dirección URL del servicio web externo.</p></td>
</tr>
<tr class="even">
<td><p><em>HybridConfigServiceInternalUrl</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Dirección URL del servicio web interno.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identidad única de las opciones de configuración híbrida del inquilino que van a modificarse. Como está limitado a una sola colección global de opciones de configuración híbrida, la única colección que se puede modificar usando el parámetro Identity es la colección global:</p>
<p>-Identity global</p>
<p>Para modificar las opciones de un inquilino concreto, use el parámetro Tenant en lugar del parámetro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Permite pasar al cmdlet una referencia a un objeto en lugar de establecer valores de parámetro independientes.</p></td>
</tr>
<tr class="odd">
<td><p><em>PeerDestination</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de dominio completo del servidor perimetral de acceso local.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuyas opciones de configuración híbrida se van a modificar. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el id. de inquilino de cada uno de los inquilinos ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si está usando una sesión remota de Windows PowerShell y solo está conectado a Skype Empresarial Online, no tiene que incluir el parámetro Tenant, pues el id. de inquilino se rellenará automáticamente en la información de conexión. El parámetro Tenant se usa, principalmente, en implementaciones híbridas.</p></td>
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

Ninguno. El cmdlet **Set-CsTenantHybridConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

Ninguno. Lo que hace el cmdlet **Set-CsTenantHybridConfiguration** es modificar las instancias existentes del objeto Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration.

## Vea también

#### Otros recursos

[Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

