---
title: Get-CsConfigurationStoreLocation
TOCTitle: Get-CsConfigurationStoreLocation
ms:assetid: abfda147-02fa-46a5-a988-d83daf4cc455
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412814(v=OCS.15)
ms:contentKeyID: 48276319
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConfigurationStoreLocation

 

_**Última modificación del tema:** 2015-03-09_

Informa la ubicación del punto de control de servicio de Active Directory de Almacén de administración central. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Get-CsConfigurationStoreLocation [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve la ruta de SQL Server al equipo (o grupo) en el que se hospeda Almacén de administración central.

    Get-CsConfigurationStoreLocation

## Ejemplo 2

El ejemplo 2 es una variación del comando del ejemplo 1. En este caso, se incluye el parámetro Report para especificar la ruta del informe que se genera al ejecutar el cmdlet **Get-CsConfigurationStoreLocation**.

    Get-CsConfigurationStoreLocation -Report "C:\Logs\ConfigurationStore.html"

## Descripción detallada

Servicios de dominio de Active Directory usa puntos de control de servicio (SCP) para ayudar a los equipos a ubicar servicios. Por ejemplo, al instalar Lync Server, se crea un punto de control de servicio que proporciona información de ubicación de Almacén de administración central, que se usa para mantener los datos de Lync Server. Equipos que necesitan obtener acceso a la base de datos para conectarse con Active Directory y usan la información que contiene el SCP para ubicar el equipo correcto y la instancia de SQL Server correspondiente.

El cmdlet **Get-CsConfigurationStoreLocation** se utiliza para informar de la ruta de SQL Server (por ejemplo, atl-sql-001.litwareinc.com/rtc) al equipo que ejecuta Almacén de administración central.

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo (FQDN) de un controlador de dominio en el que se almacena la configuración global. Si la configuración global se almacena en el contenedor del sistema de Active Directory, este parámetro debe hacer referencia al controlador de dominio raíz. Si la configuración global está almacenada en el contenedor de configuración, se puede usar cualquier controlador de dominio y omitir este parámetro.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite especificar una ruta de archivo para el archivo de registro creado al iniciar el cmdlet. Por ejemplo: -Report &quot;C:\Registros\AlmacenConfiguracion.html&quot;</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Get-CsConfigurationStoreLocation** no acepta entradas canalizadas.

## Tipos de valores devueltos

Cadena. El cmdlet **Get-CsConfigurationStoreLocation** notifica la ubicación del almacén de configuraciones.

## Vea también

#### Otros recursos

[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

