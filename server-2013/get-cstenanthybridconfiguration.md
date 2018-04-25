---
title: Get-CsTenantHybridConfiguration
TOCTitle: Get-CsTenantHybridConfiguration
ms:assetid: 4b2e6781-8f46-4ba3-be76-3a95460e3132
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994034(v=OCS.15)
ms:contentKeyID: 52061680
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantHybridConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Devuelve valores para las opciones de configuración híbrida que permiten a los usuarios hospedados en Microsoft Lync Online obtener acceso a las funciones de Telefonía IP empresarial, como la omisión de medios, el 9-1-1 mejorado y el estacionamiento de llamadas. Un escenario híbrido (también conocido como escenario de dominio dividido) es una implementación de Lync Server en la que algunos usuarios tienen cuentas hospedadas localmente y otros usuarios tienen cuentas hospedadas en Lync Online.

El cmdlet Get-CsTenantHybridConfiguration solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Get-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-LocalStore] [<CommonParameters>]Get-CsTenantHybridConfiguration [-Tenant <guid>] [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve los valores de propiedad para la colección global de opciones de configuración híbrida del inquilino.

    Get-CsTenantHybridConfiguration -Identity "Global"

## Ejemplo 2

En el ejemplo 2, los valores de propiedad que se devuelven corresponden a las opciones de configuración híbrida del inquilino que se aplican al inquilino cuyo TenantId es "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## Ejemplo 3

El ejemplo 3 devuelve información de configuración híbrida de inquilino sobre todos los inquilinos disponibles. Para hacer esto, el comando llama primero al cmdlet **Get-CsTenant** para devolver una colección de todos estos inquilinos. Luego, esta colección se canaliza al cmdlet **ForEach-Object**, que toma cada uno de los inquilinos de la colección y realiza en ellos, por separado, dos tareas. Primero, el cmdlet imprime el nombre para mostrar de Active Directory del inquilino; esto garantiza que todas las colecciones de opciones se identifiquen fácilmente. Después, el cmdlet **ForEach-Object** ejecuta el cmdlet **Get-CsTenantHybridConfiguration** para devolver las opciones de configuración híbrida del inquilino para el inquilino en cuestión.

    Get-CsTenant | ForEach-Object {$_.DisplayName; Get-CsTenantHybridConfiguration -Tenant $_.TenantId}

## Descripción detallada

En una implementación híbrida o de "dominio dividido", una organización tiene algunos usuarios con cuentas hospedadas en Lync Online, mientras que otros usuarios tienen cuentas hospedadas en la versión local de Lync Server. De manera predeterminada, los usuarios hospedados en Lync Online no tienen acceso a la gama completa de capacidades que ofrece Telefonía IP empresarial. Esto se debe a que los servidores de Lync Online no tienen acceso directo a la información de configuración de red y de implementación de Lync Server. Los usuarios de Lync Online no tienen acceso predeterminado, entre otras cosas, a:

  - 9-1-1 mejorado, el servicio de Lync Server usado para hacer llamadas de emergencia.

  - Estacionamiento de llamadas, el servicio de Lync Server que permite a los usuarios poner una llamada en espera en el teléfono A y recuperarla después desde el teléfono B.

  - Omisión de medios, que permite que las llamadas hechas y recibidas a través de la red telefónica conmutada (RTC) omitan el servidor de mediación, lo cual sirve para minimizar la latencia de red y la transcodificación.

  - Funciones para realizar y recibir llamadas de RTC, que permiten a los usuarios participar en la parte de audio de una conferencia en línea usando un teléfono de RTC o un dispositivo móvil.

  - La aplicación de grupo de respuesta, que permite enrutar automáticamente las llamadas telefónicas a entidades, como una línea de asistencia técnica o atención al cliente. De manera predeterminada, los usuarios de Lync Server no pueden actuar como agentes de grupo de respuesta.

Para ofrecer a los usuarios de Lync Online acceso a estas capacidades de Telefonía IP empresarial, los administradores tienen que asignar los valores apropiados a las opciones de configuración híbrida, como las direcciones URL del servicio web interno y externo, y el nombre de dominio completo del servidor perimetral de acceso de la organización. Estos valores, que solo se pueden configurar usando el cmdlet **Set-CsTenantHybridConfiguration**, dan a los servidores de Lync Online la información necesaria para hacer uso de estas funciones avanzadas de Telefonía IP empresarial.

Puede devolver información sobre las opciones de configuración híbrida del inquilino que se están usando actualmente en la organización con el cmdlet **Get-CsTenantHybridConfiguration**.

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
<td><p>Le permite usar caracteres comodín para devolver una colección de opciones de configuración híbrida de inquilino. Como existe la limitación de una sola colección global de opciones de configuración híbrida, no es necesario usar el parámetro Filter. Sin embargo, esta sintaxis es válida para el cmdlet <strong>Get-CsTenantHybridConfiguration</strong>:</p>
<p>Get-CsTenantHybridConfiguration –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identidad única de la opción de configuración híbrida de inquilino que se va a devolver. Como existe la limitación de una sola colección global de opciones de configuración híbrida, la única colección que se puede devolver usando el parámetro Identity es la colección global:</p>
<p>-Identity global</p>
<p>Para modificar las opciones de un inquilino concreto, use el parámetro Tenant en lugar del parámetro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera los datos de configuración híbrida del inquilino a partir de la réplica local del Almacén de administración central en lugar de hacerlo a partir del propio almacén.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuyas opciones de configuración híbrida se van a devolver. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el id. del inquilino para cada uno de los inquilinos inicie este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si mantiene una sesión remota de Windows PowerShell y solo se ha conectado a Skype Empresarial Online, no tiene que incluir el parámetro Tenant. De hecho, el identificador de inquilino se rellenará automáticamente a partir de la información de conexión en uso. Por lo general, el parámetro Tenant se usa en implementaciones híbridas.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsTenantHybridConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Get-CsTenantHybridConfiguration** devuelve instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration.

## Vea también

#### Otros recursos

[Set-CsTenantHybridConfiguration](set-cstenanthybridconfiguration.md)

