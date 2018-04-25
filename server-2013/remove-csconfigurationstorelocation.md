---
title: Remove-CsConfigurationStoreLocation
TOCTitle: Remove-CsConfigurationStoreLocation
ms:assetid: 141be225-c6e4-4377-913b-ba61528929d4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398214(v=OCS.15)
ms:contentKeyID: 48274512
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConfigurationStoreLocation

 

_**Última modificación del tema:** 2015-03-09_

Quita el punto de control del servicio Active Directory para la Almacén de administración central. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Remove-CsConfigurationStoreLocation [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

El comando que aparece en el ejemplo 1 quita el punto de control del servicio de Active Directory para la Almacén de administración central. Para restaurar este punto de control del servicio (o crear uno nuevo), deberá ejecutar el cmdlet **Set-CsConfigurationStoreLocation**.

    Remove-CsConfigurationStoreLocation

## EJEMPLO 2

En el ejemplo 2 también se quita el punto de control del servicio Active Directory para la Almacén de administración central. Además de eliminarlo, este comando registra información acerca del éxito (o fracaso) de la operación en el archivo de registro C:\\Store\_Location.html. Para crear este archivo de registro, el comando usa el parámetro Report seguido de la ruta al archivo de registro en el que se deberá grabar la información. Si este archivo ya existe, el contenido se sobrescribirá al ejecutar el comando. Si el archivo no existe, se creará al ejecutar el comando.

    Remove-CsConfigurationStoreLocation -Report C:\Logs\Store_Location.html

## Descripción detallada

Servicios de dominio de Active Directory usa puntos de control de servicio (SCP) para ayudar a los equipos a ubicar servicios. Por ejemplo, al instalar Lync Server, se crea un punto de control del servicio que proporciona información de ubicación para la Almacén de administración central que se usa para mantener los datos de Lync Server. Los equipos que necesitan obtener acceso a la base de datos se conectan a Active Directory y usan la información que contiene el SCP para encontrar el equipo correcto y la instancia de SQL Server correspondiente.

Tal como se ha indicado, al instalar Lync Server, se crea automáticamente un SCP para Almacén de administración central. Normalmente, no será conveniente eliminarlo, ya que si lo hace, los equipos no podrán encontrar la base de datos. Sin embargo, puede haber ocasiones (por ejemplo, al solucionar un problema) en las que necesitará hacerlo. Para ello, use el cmdlet **Remove-CsConfigurationStoreLocation**. Una vez eliminado el SCP, puede volver a crearlo (o crear un punto de control de servicio nuevo) con el cmdlet **Set-CsConfigurationStoreLocation**.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Remove-CsConfigurationStoreLocation** localmente: RTCUniversalServerAdmins.

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
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no son graves y que pueden surgir al ejecutar el comando.</p></td>
</tr>
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
<td><p>Permite especificar la ruta de acceso del archivo de registro que se crea al ejecutarse el cmdlet. Por ejemplo: -Report &quot;C:\Registros\AlmacenConfiguracion.html&quot;</p></td>
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

Ninguno. El cmdlet **Remove-CsConfigurationStoreLocation** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Remove-CsConfigurationStoreLocation** no devuelve objetos ni valores.

## Vea también

#### Otros recursos

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

