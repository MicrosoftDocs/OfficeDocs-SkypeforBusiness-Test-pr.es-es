---
title: Import-CsConfiguration
TOCTitle: Import-CsConfiguration
ms:assetid: 9a9c27f2-313c-4327-aeed-c47852a831ec
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398800(v=OCS.15)
ms:contentKeyID: 48276204
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Importa la topología, las directivas y las opciones de configuración de Lync Server a Almacén de administración central o al equipo local. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Import-CsConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    Import-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Ejemplos

## Ejemplo 1

El comando anterior importa la topología, las opciones de configuración y las directivas actuales de un archivo llamado C:\\Config.zip a Almacén de administración central.

    Import-CsConfiguration -FileName "C:\Config.zip"

## Ejemplo 2

En el ejemplo2 se muestra la forma en la que se puede replicar datos inicialmente en un equipo de la red perimetral. En este ejemplo, los datos de configuración se han exportado a un archivo llamado Config.zip; este archivo se ha copiado a la carpeta C:\\ del equipo de la red perimetral. A continuación, Import-CsConfiguration se usa para importar esos datos, con el parámetro LocalStore, lo que hace que los datos se importen al PC local en lugar de a Almacén de administración central.

    Import-CsConfiguration -FileName "C:\Config.zip" -LocalStore

## Ejemplo 3

Los dos comandos que aparecen en el ejemplo 3 exportan la topología, los parámetros de configuración y las directivas actuales y luego exportan esos datos al equipo local, todo sin usar un archivo .ZIP. Para ello, el comando usa el cmdlet **Export-CsConfiguration** y el parámetro AsBytes para exportar la topología, los parámetros de configuración y las directivas actuales como una matriz de bytes; esta matriz de bytes se almacena en una variable llamada $x. En el segundo comando, se usan el cmdlet **Import-CsConfiguration** y el parámetro ByteInput para importar información almacenada en $x. El parámetro LocalStore hace que los datos se importen al equipo local en lugar de importarse a Almacén de administración central. El resultado final es que los datos se copian de Almacén de administración central al equipo local.

    $x = Export-CsConfiguration -AsBytes
    Import-CsConfiguration -ByteInput $x -LocalStore

## Descripción detallada

Los PC que inician roles de servidores o servicios de Lync Server deben tener una copia de la topología, las opciones de configuración y las directivas actuales, entre otros, para poder funcionar en su rol asignado. Lync Server tiene la función de garantizar que la información se pase a todos los PC que la necesiten.

Los cmdlets Import-CsConfiguration y Export-CsConfiguration se usan para crear copias de seguridad y restaurar la topología, los parámetros de configuración y las directivas de Lync Server durante la actualización del Almacén de administración central. El cmdlet **Export-CsConfiguration** permite exportar datos a un archivo .ZIP; luego, puede usar el cmdlet **Import-CsConfiguration** para leer el archivo .ZIP y restaurar la topología, los parámetros de configuración y las directivas al Almacén de administración central. Luego, los servicios de replicación de Lync Server replicarán la información restaurada en los equipos que usan servicios.

La capacidad de exportar e importar datos de configuración también se usa en la configuración inicial de los equipos de su red perimetral (por ejemplo, Servidor perimetral). Al configurar un equipo de la red perimetral, primero debe realizar una replicación manual con los cmdlets CsConfiguration. Deberá exportar los datos de configuración con el cmdlet **Export-CsConfiguration** y después copiar el archivo .ZIP al equipo de la red perimetral. Luego, puede usar el cmdlet **Import-CsConfiguration** y el parámetro LocalStore para importar los datos. Solo será necesario hacerlo una vez; después, la replicación se ejecutará automáticamente.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los grupos siguientes están autorizados a iniciar el cmdlet **Import-CsConfiguration** localmente: RTCUniversalServerAdmins. Para ejecutar este cmdlet, además de ser miembro de RTCUniversalServerAdmins, debe ser administrador local o tener permisos de replicador de la configuración local. Para obtener una lista de todos los roles de control de acceso basado en roles (RBAC) que se han asignado a este cmdlet (incluidos los roles RBAC personalizados que haya creado), inicie el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsConfiguration"}

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
<td><p><em>ByteInput</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Lee la información de topología de una matriz de bytes almacenada en una variable. Esta matriz de bytes se crea al usar el parámetro ByteInput cuando se llama al cmdlet <strong>Export-CsConfiguration</strong>.</p>
<p>No se pueden usar ambos parámetros ByteInput y FileName dentro del mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ruta de acceso al archivo .ZIP creada por Export-CsConfiguration. Por ejemplo: -FileName &quot;C:\Config.zip&quot;. Recuerde que debe incluir los parámetros FileName o ByteInput, pero no ambos, al llamar al cmdlet <strong>Import-CsConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Omite las indicaciones que aparecerían en caso de producirse un error que no es grave al ejecutar el comando. Para definir el parámetro Force en True, use esta sintaxis:</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Copia los datos de configuración en el PC local en lugar de hacerlo en Almacén de administración central.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **Import-CsConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **Import-CsConfiguration** no devuelve ningún valor u objeto.

## Vea también

#### Otros recursos

[Export-CsConfiguration](export-csconfiguration.md)

