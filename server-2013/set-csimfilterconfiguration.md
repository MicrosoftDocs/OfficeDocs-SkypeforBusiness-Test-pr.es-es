---
title: Set-CsImFilterConfiguration
TOCTitle: Set-CsImFilterConfiguration
ms:assetid: c2b08cc0-8261-4b8b-b2e9-5efa902ceb40
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412960(v=OCS.15)
ms:contentKeyID: 48276576
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsImFilterConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Modifica una configuración de filtro de mensajería instantánea (MI) existente. La configuración de filtro de mensajería instantánea se usa para impedir que los usuarios envíen mensajes instantáneos que contengan hipervínculos activos (en los que se pueda hacer clic). Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsImFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando de este ejemplo deshabilita el filtrado URI para la configuración de filtro de IM con la identidad site:Redmond. Para realizar esta tarea, se especifica el parámetro Enabled en la llamada al cmdlet **Set-CsImFilterConfiguration** con un valor de $False.

    Set-CsImFilterConfiguration -Identity site:Redmond -Enabled $False

## Ejemplo 2

El conjunto anterior de comandos agrega un prefijo URI nuevo (urn:) a la lista de prefijos prohibidos por la configuración de filtro de IM de site:Redmond. Para agregar el nuevo prefijo, se usa el cmdlet **Get-CsImFilterConfiguration** para recuperar la configuración de site:Redmond; el objeto devuelto que representa dicha configuración se almacena en una variable denominada $x. Una vez recuperada la configuración, se llama al método Add() en la línea 2 para agregar urn: al conjunto de prefijos almacenados en la propiedad Prefixes. De este forma, se cambia el valor de la referencia al objeto $x. Para cambiar la configuración real, en la línea 3 se llama al cmdlet **Set-CsImFilterConfiguration**, donde se envía $x como valor único del parámetro.

    $x = Get-CsImFilterConfiguration -Identity site:Redmond
    $x.Prefixes.Add("urn:")
    Set-CsImFilterConfiguration -Instance $x

## Ejemplo 3

En el ejemplo 3 se lleva a cabo la misma acción que en el ejemplo 2, pero en una sola línea. En este comando el parámetro -Prefixes del cmdlet **Set-CsImFilterConfiguration** se usa para agregar urn: a la lista de prefijos. El modificador de lista add se usa para agregar este valor a la lista Prefixes.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="urn:"}

## Ejemplo 4

En este ejemplo, el prefijo urn: se quita de la lista de prefijos bloqueados por la configuración de filtro de mensajería instantánea de site:Redmond. Este ejemplo es idéntico al ejemplo 3, excepto por el hecho que en lugar de llamar al modificador de lista add para agregar un prefijo a la lista, se llama al modificador remove para quitar un prefijo.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{remove="urn:"}

## Descripción detallada

Al enviar mensajes instantáneos, los usuarios pueden insertar un Identificador de recursos uniforme (URI) en el texto del mensaje para compartir un sitio web o un recurso compartido determinado con el resto de participantes de la conversación. Lync Server se puede configurar de modo que los hipervínculos que contengan determinados prefijos se bloqueen o no estén activos. (En otras palabras, los participantes no pueden limitarse a hacer clic en el vínculo y obtener acceso al sitio al que refiera el URI; deben copiar y pegar el vínculo de forma manual a un explorador).

El cmdlet **Set-CsImFilterConfiguration** permite modificar una lista de prefijos URI que se filtrarán, así como habilitar y deshabilitar el filtrado por completo, globalmente o dentro de un sitio específico. Con este cmdlet también puede actualizar varios mensajes de advertencia a los usuarios.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsImFilterConfiguration** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsImFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>Opcional</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>El valor de este parámetro determina la acción que se llevará a cabo cuando se incluya un hipervínculo en un mensaje instantáneo:</p>
<p>Allow: los hipervínculos van precedidos de un carácter de subrayado para que los vínculos dejen de estar activos. Además, si se especifica un mensaje en la propiedad AllowMessage, se inserta un mensaje de notificación al principio de cada mensaje instantáneo que contenga hipervínculos.</p>
<p>Block: se bloquea la entrega de mensajes que contengan hipervínculos activos y Lync Server envía un mensaje de error al remitente.</p>
<p>Warn: los mensajes que contengan hipervínculos activos se entregan a los participantes receptores, junto con un mensaje de advertencia que se inserta al inicio de dichos mensajes. El mensaje de advertencia puede especificarse con la propiedad WarnMessage. Si se especifica Warn y no se introduce ningún mensaje WarnMessage, se deshabilitará el filtrado de mensajería instantánea, a pesar de que la configuración de la propiedad BlockFileExtension se continuará respetando.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowMessage</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Si se especifica un valor para este parámetro, la cadena de caracteres se insertará al inicio de cada mensaje que contenga hipervínculos siempre que el valor de la propiedad Action esté definido en Allow. Puede usar este mensaje para informar a los usuarios sobre aspectos como los posibles riesgos de hacer clic en vínculos desconocidos o las directivas y los requisitos correspondientes a la organización.</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Si este parámetro está definido en True, se bloquearán los hipervínculos que contengan una ruta de archivo con una extensión especificada con la propiedad Extensions definida en la clase Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration (recuperada llamando al cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>) y el remitente recibirá un mensaje de error. Si este parámetro está definido en False, no se realizará ninguna comprobación especial para las rutas de archivo y extensiones.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Habilita o deshabilita esta característica. Si este parámetro se define en True, se analizarán los mensajes instantáneos en busca de hipervínculos y se aplicarán las reglas incluidas en esta configuración. Si este parámetro se define en False, no se comprobarán los mensajes en busca de hipervínculos.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>El identificador único de las opciones de configuración de filtro de mensajería instantánea que se quieren modificar. Este valor será global o site:&lt;nombre del sitio&gt;, donde &lt;nombre del sitio&gt; es el sitio al que se aplica la configuración, como site:Redmond.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>El valor de este parámetro controla si el filtrado se realiza en los URI de la intranet local enviados en los mensajes instantáneos. Si está definido en True, se omitirán todos los URI que se hayan definido en la zona de intranet del PC local. (El PC local es el equipo Servidor front-end que ejecuta la aplicación de filtro de mensajería instantánea). Si este parámetro está definido en False, el filtrado especificado se aplica a todos los hipervínculos.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>ImFilterConfiguration</p></td>
<td><p>Permite enviar una referencia a un objeto al cmdlet, en lugar de definir valores de parámetros individuales. Este cmdlet acepta un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration, que se puede recuperar llamando al cmdlet <strong>Get-CsImFilterConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>La lista de prefijos URI que se filtrará. Todos los hipervínculos incluidos en un mensaje instantáneo con un prefijo que coincida con uno de los prefijos de la lista se filtrarán de acuerdo con la configuración especificada.</p>
<p>Valor predeterminado: callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*.</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Este parámetro contiene el mensaje de advertencia que se inserta al principio de todos los mensajes instantáneos que contienen hipervínculos, si el valor de la propiedad Action está definido en Warn. Normalmente, este mensaje se usa para indicar los posibles riesgos de hacer clic en vínculos desconocidos o para hacer referencia a directivas o requisitos relevantes para la organización.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration. Acepta la entrada canalizada de objetos de configuración de filtro de mensajería instantánea.

## Tipos de valores devueltos

El cmdlet **Set-CsImFilterConfiguration** no devuelve ningún valor u objeto. En su lugar, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Vea también

#### Otros recursos

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

