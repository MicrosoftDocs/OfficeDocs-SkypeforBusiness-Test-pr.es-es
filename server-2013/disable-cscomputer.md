---
title: Disable-CsComputer
TOCTitle: Disable-CsComputer
ms:assetid: e64128f1-2b53-4569-bf37-90cbbba01b36
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399023(v=OCS.15)
ms:contentKeyID: 48276987
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsComputer

 

_**Última modificación del tema:** 2015-03-09_

Deshabilita un servicio o rol de servidor que se ha quitado de un equipo con Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Disable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Scorch <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 deshabilita el equipo local.

    Disable-CsComputer 

## Ejemplo 2

El comando del ejemplo 2 también deshabilita el equipo local. Además de deshabilitar el equipo, este comando registra información sobre si la tarea se ha ejecutado correctamente, o ha fallado, en el archivo C:\\Logs\\Disable.html. Este archivo de registro se genera agregando el parámetro Report seguido de la ruta de acceso al archivo de registro en el que desea almacenar la información.

    Disable-CsComputer -Report C:\Logs\Disable.html

## Descripción detallada

Al quitar un servicio o un rol del servidor de un equipo, no se actualiza automáticamente la topología de Lync Server. Por el contrario, se debe deshabilitar el servicio o rol antes de que los cambios se actualicen completamente en la topología. El cmdlet **Disable-CsComputer** permite a los administradores deshabilitar cualquier servicio o rol de servidor que se haya quitado del equipo local.

Salvo que se use el parámetro Scorch, el cmdlet **Disable-CsComputer** no desinstala el software Lync Server; solamente hace que el equipo deje de funcionar en el rol asignado anteriormente.

Quién puede ejecutar este cmdlet: Para ejecutar localmente el cmdlet **Disable-CsComputer**, debe ser un administrador local y un miembro del dominio.

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
<th>Requerido</th>
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
<td><p>Suprime la visualización de los mensajes de error que no sean irrecuperables y que puedan surgir al ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo (FQDN) de un servidor de catálogo global del dominio. Este parámetro no es obligatorio si ejecuta el cmdlet <strong>Disable-CsComputer</strong> en un equipo con una cuenta de su dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nombre de dominio completo de un controlador de dominio donde están almacenadas las configuraciones globales. Si la configuración global se almacena en el contenedor del sistema de Servicios de dominio de Active Directory, este parámetro debe hacer referencia al controlador de dominio raíz. Si la configuración global está almacenada en el contenedor de configuración, se puede usar cualquier controlador de dominio y omitir este parámetro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Permite especificar la ruta del archivo de registro creado al ejecutar el cmdlet. Por ejemplo: -Report &quot;C:\Logs\DisableComputer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scorch</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Desinstala todos los servicios y roles de servidor de Lync Server del equipo local.</p></td>
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

Ninguno. El cmdlet **Disable-CsComputer** no acepta entradas canalizadas.

## Tipos de valores devueltos

Ninguno. El cmdlet **Disable-CsComputer** deshabilita instancias del objeto Microsoft.Rtc.Management.Deploy.Internal.Machine.

## Vea también

#### Otros recursos

[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

