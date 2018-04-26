---
title: New-CsImFilterConfiguration
TOCTitle: New-CsImFilterConfiguration
ms:assetid: 1964cbf9-d7f1-4b4e-99d1-951ac42d82fe
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398244(v=OCS.15)
ms:contentKeyID: 48274573
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsImFilterConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea una nueva configuración del filtro de mensajería instantánea (MI). Los filtros de MI sirven para evitar que los usuarios envíen mensajes instantáneos con hipervínculos activos. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsImFilterConfiguration -Identity <XdsIdentity> [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-InMemory <SwitchParameter>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En el ejemplo 1, el cmdlet **New-CsImFilterConfiguration** se usa para crear una nueva configuración de filtro de MI con la identidad site:Redmond. (Como no se especifican parámetros adicionales, estas opciones se crearán con los valores predeterminados).

    New-CsImFilterConfiguration -Identity site:Redmond

## EJEMPLO 2

En este comando, el cmdlet **New-CsImFilterConfiguration** se usa para crear una nueva configuración de filtro de MI con la identidad site:Redmond. Como se ha especificado el parámetro Prefixes, la nueva configuración incluirá todos los valores predeterminados, incluidos los prefijos predeterminados para filtrar, más dos prefijos URI adicionales: rtsp: y urn:. Estos prefijos se agregan a la lista predeterminada con el modificador de la lista de adiciones.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="rtsp:","urn:"}

## EJEMPLO 3

En este comando, el cmdlet **New-CsFileTransferFilterConfiguration** se usa para crear una nueva configuración de filtro de MI con la identidad site:Redmond. Este ejemplo es similar al ejemplo 2, salvo que se ha utilizado el modificador de la lista de sustituciones en lugar del modificador de la lista de adiciones. Esto significa que todos los prefijos URI predeterminados se sustituirán por estos dos prefijos (rtsp: y urn:). Por consiguiente, solo se filtrarán los URI con prefijos de rtsp: o urn: en los mensajes instantáneos para el sitio Redmond.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{replace="rtsp:","urn:"}

## Descripción detallada

Al enviar mensajes instantáneos, los usuarios pueden insertar un URI en el texto del mensaje para compartir un sitio web o un recurso compartido determinado con el resto de participantes de la conversación. Lync Server se puede configurar de modo que los hipervínculos que contengan determinados prefijos se bloqueen o no estén activos. (En otras palabras, los participantes no pueden simplemente hacer clic en el vínculo y obtener acceso al sitio al que el URI haga referencia, sino que deben copiar y pegar el vínculo manualmente en un explorador).

El cmdlet **New-CsImFilterConfiguration** permite al usuario definir una lista de prefijos URI que se filtrarán (así como habilitar y deshabilitar el filtrado en general) en un sitio específico. Si se llama al cmdlet **New-CsImFilterConfiguration** con un único parámetro Identity especificado, se creará una nueva configuración con dicha identidad y se rellenará la lista de prefijos de ese sitio con un conjunto de prefijos predeterminados que se filtrarán.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **New-CsImFilterConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsImFilterConfiguration"}

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
<td><p>Obligatorio</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificador único que identifica el ámbito de la configuración del filtro de mensajería instantánea. La configuración global existe de manera predeterminada y no puede volver a crearse con el cmdlet <strong>New-CsImFilterConfiguration</strong>, si bien el usuario puede crear configuraciones de nivel del sitio especificando un parámetro Identity igual a site:&lt;nombre del sitio&gt;, donde &lt;nombre del sitio&gt; es el nombre del sitio al que se aplicará la configuración (por ejemplo, site:Redmond).</p>
<p>Tipo de datos completo: Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>Opcional</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>El valor de este parámetro determina la acción que se llevará a cabo cuando se incluya un vínculo en un mensaje instantáneo:</p>
<p>Allow: los hipervínculos van precedidos de un carácter de subrayado de modo que ya no estén activos. Si se especifica un mensaje en la propiedad AllowMessage, este se podrá insertar al principio de cada mensaje instantáneo que contenga hipervínculos.</p>
<p>Block: se bloquea la entrega de mensajes que contengan hipervínculos activos y Lync Server envía un mensaje de error al remitente.</p>
<p>Warn: los mensajes que contienen hipervínculos activos se entregan a los participantes receptores, junto con un mensaje de advertencia que se inserta al principio de dichos mensajes. El mensaje de advertencia puede especificarse con la propiedad WarnMessage. Si se especifica Warn y no se introduce ningún WarnMessage, el filtrado de mensajería instantánea se inhabilitará, aunque la configuración de la propiedad BlockFileExtension se seguirá teniendo en cuenta.</p>
<p>Valor predeterminado: Permitir, a menos que un mensaje contenga más de 1.000 URL, en cuyo caso la opción predeterminada será Bloquear.</p>
<p>Tipo de datos completo: Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.UrlFilterAction</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMessage</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Si se especifica un valor para este parámetro, esa cadena se insertará al principio de todos los mensajes que contengan hipervínculos cuando el valor de la propiedad Action esté establecido en Allow. Puede usar este mensaje para informar a los usuarios de aspectos como los posibles riesgos de hacer clic en vínculos desconocidos o las directivas y los requisitos correspondientes a la organización.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Si este parámetro está establecido en True, se bloquearán los hipervínculos que contengan una ruta de acceso de archivo con una extensión especificada mediante la propiedad Extensions definida en la configuración de filtro de transferencia de archivo aplicable (que se puede obtener llamado al cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>) y el remitente recibirá un mensaje de error. Si este parámetro está establecido en False, no se realizará ninguna comprobación especial de las extensiones de archivo.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Habilita o inhabilita esta característica. Si este parámetro está establecido en True, se examinarán los mensajes instantáneos para comprobar si contienen hipervínculos y se aplicarán las reglas establecidas en esta configuración. Si este parámetro está establecido en False, no se comprobará si los mensajes contienen hipervínculos.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>El valor de este parámetro controla si el filtrado se lleva a cabo en los URI de Intranet locales enviadas en los mensajes instantáneos. Si este parámetro está establecido en True, se ignorarán todos los URI definidos en la zona de Intranet del equipo local. (El equipo local es el Servidor front-end que ejecuta la aplicación de filtro de MI.) Si este parámetro está establecido en False, el filtrado especificado se aplica a todos los hipervínculos.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>La lista de prefijos URI que se filtrarán. Todos los hipervínculos incluidos en un mensaje instantáneo que tengan un prefijo que coincida con uno de los prefijos de esta lista se filtrarán de acuerdo con la configuración especificada.</p>
<p>Valor predeterminado: callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*.</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Este parámetro contiene el mensaje de advertencia que se inserta al principio de los mensajes instantáneos que incluyen hipervínculos cuando el valor de la propiedad Action está establecido en Warn (Advertencia). Normalmente, este mensaje se usa para indicar los posibles riesgos de hacer clic en vínculos desconocidos o para hacer referencia a directivas o requisitos relevantes para la organización.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno.

## Tipos de valores devueltos

Crea un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Vea también

#### Otros recursos

[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

