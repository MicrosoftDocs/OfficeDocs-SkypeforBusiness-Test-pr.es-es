---
title: Set-CsConfigurationStoreLocation
TOCTitle: Set-CsConfigurationStoreLocation
ms:assetid: 1c69a872-8e78-4c78-ba27-f20f04dce59f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398258(v=OCS.15)
ms:contentKeyID: 48274602
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConfigurationStoreLocation

 

_**Última modificación del tema:** 2015-03-09_

Define el punto de control del servicio Active Directory para Almacén de administración central. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsConfigurationStoreLocation -SqlServerFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-MirrorSqlInstanceName <String>] [-MirrorSqlServerFqdn <Fqdn>] [-Report <String>] [-SkipLookup <SwitchParameter>] [-SqlInstanceName <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

El comando que se muestra en el ejemplo 1 configura el punto de control de servicio de Active Directory para Lync Server Almacén de administración central. En este ejemplo, el SCP se refiere al equipo atl-sql-001.litwareinc.com y a la instancia de SQL Server Rtc.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc

## EJEMPLO 2

El comando que se muestra en el ejemplo 2 es una variación del comando que se muestra en el ejemplo 1. Este comando además configura el SCP de Active Directory para Lync Server Almacén de administración central. Además, la información acerca del resultado correcto (o con error) de la operación se registra en el archivo C:\\Logs\\Store\_Location.html. Este registro se genera al incluir el parámetro -Report seguido de la ruta de acceso completa al archivo de registro.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc -Report C:\Logs\Store_Location.html

## Descripción detallada

Servicios de dominio de Active Directory usa puntos de control de servicio (SCP) para ayudar a los equipos a ubicar servicios. Por ejemplo, cuando instala Lync Server, se crea un punto de control de servicio que proporciona información sobre la ubicación del Almacén de administración central que se usa para mantener datos de Lync Server. Los equipos que necesitan obtener acceso a la base de datos se conectan con Active Directory y usan la información que contiene el punto de control de servicio para ubicar el equipo correcto y la instancia de SQL Server correspondiente.

Como se ha indicado, cuando se instala Lync Server se crea automáticamente un punto de control de servicio para Almacén de administración central. Si necesita mover la base de datos a otro equipo o a otra instancia de SQL Server, deberá actualizar el punto de control de servicio correspondiente. Esa tarea puede realizarse con el cmdlet **Set-CsConfigurationStoreLocation**. Al ejecutarlo, el cmdlet **Set-CsConfigurationStoreLocation** busca en Active Directory el equipo especificado por el parámetro SqlServer. A continuación, establece la ubicación de almacenamiento en el FQDN de ese equipo.

Quiénes pueden ejecutar este cmdlet: De manera predeterminada, los miembros de los siguientes grupos están autorizados para ejecutar el cmdlet **Set-CsConfigurationStoreLocation** en forma local: RTCUniversalServerAdmins.

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
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo (FQDN) del equipo donde se ha instalado Almacén de administración central. Por ejemplo: -SqlServer atl-sql-001.litwareinc.com.</p></td>
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
<td><p>Suprime la visualización de los mensajes de error que no sean graves y que puedan producirse al ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo de un controlador de dominio donde se almacenan las configuraciones globales. Si la configuración global se almacena en el contenedor del sistema de Active Directory, este parámetro debe hacer referencia al controlador de dominio raíz. Si la configuración global está almacenada en el contenedor de configuración, se puede usar cualquier controlador de dominio y omitir este parámetro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorSqlInstanceName</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de la instancia de SQL Server que contiene las tablas y los datos de la base de datos reflejada de Lync Server. Por ejemplo: -SqlInstanceName &quot;rtc&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorSqlServerFqdn</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo (FQDN) del equipo donde se ha instalado la base de datos reflejada de Almacén de administración central. Por ejemplo: -SqlServer atl-mirror-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Le permite especificar una ruta de acceso para el archivo de registro creado cuando se ejecuta el cmdlet. Por ejemplo: -Report &quot;C:\Registros\AlmacenConfiguracion.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipLookup</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Si se incluye este parámetro, el cmdlet <strong>Set-CsConfigurationStoreLocation</strong> no comprobará que el equipo y la instancia de SQL Server especificados se encuentren disponibles. En lugar de ello, simplemente cambiará el punto de control de servicio.</p>
<p>Si este parámetro no se incluye, tanto el equipo como la instancia de SQL Server deben estar disponibles para que se modifique el SCP.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de la instancia de SQL Server que contiene las tablas y los datos de Lync Server. Por ejemplo: -SqlInstanceName &quot;rtc&quot;.</p></td>
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

Ninguno. El cmdlet **Set-CsConfigurationStoreLocation** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Set-CsConfigurationStoreLocation** no devuelve valores ni objetos.

## Vea también

#### Otros recursos

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

