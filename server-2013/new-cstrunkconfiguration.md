---
title: New-CsTrunkConfiguration
TOCTitle: New-CsTrunkConfiguration
ms:assetid: f3958f86-3313-4929-9f9d-f796a2669aea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg413021(v=OCS.15)
ms:contentKeyID: 48277156
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrunkConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea una nueva configuración troncal que describe la configuración para una entidad troncal del mismo tipo, como una puerta de enlace de red telefónica conmutada (RTC), un sistema PBX (Public Branch eXchange) IP o un controlador SBC (Session Border Controller) en el proveedor de servicios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsTrunkConfiguration -Identity <XdsIdentity> [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-InMemory <SwitchParameter>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se crea una configuración troncal con el valor de Identity site:Redmond. Las propiedades restantes de esta nueva configuración se rellenarán con los valores predeterminados.

    New-CsTrunkConfiguration -Identity site:Redmond

## Ejemplo 2

En este ejemplo se crea una configuración troncal con el valor de Identity site:Redmond y se habilita la omisión de medios. La omisión de medios se habilita asignando el valor $True al parámetro EnableBypass. Las propiedades restantes de esta nueva configuración se rellenarán con los valores predeterminados.

    New-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## Ejemplo 3

En este ejemplo, se crea una configuración de tronco con el valor de Identity site:Redmond y, a continuación, se asigna una nueva conversión saliente a ese tronco. En la primera línea del ejemplo, se llama al cmdlet **New-CsTrunkConfiguration** para crear la configuración de tronco con los valores predeterminados. En la segunda línea, se llama al cmdlet **New-CsOutboundTranslationRule**. Preste atención al valor asignado a la identidad: site:Redmond/OTR1. La primera parte de la identidad (site:Redmond) define el ámbito en el que se aplica la regla. Dicho ámbito coincide con el valor de Identity de la nueva configuración de tronco, lo que significa que esta regla se aplicará automáticamente a esa configuración. El ámbito va seguido de una barra diagonal (/) y una cadena, que no es más que el nombre único de esta regla (puede haber más de una regla en cada ámbito). Después de esto, se transfieren los valores a los parámetros Pattern y Translation para definir la regla.

    New-CsTrunkConfiguration -Identity site:Redmond
    New-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Pattern '^\+(\d{8})$' -Translation '9$1'

## Descripción detallada

Use este cmdlet para crear una configuración troncal aplicable a las entidades de puerta de enlace RTC. Cada configuración contiene opciones de configuración específicas para una entidad troncal del mismo tipo, como una puerta de enlace RTC, un sistema IP-PBX o un controlador SBC en el proveedor de servicios. Esta configuración establece aspectos, por ejemplo, si la omisión de medios está habilitada en este tronco, si los paquetes del protocolo de transporte en tiempo real (RTCP) se envían bajo determinadas condiciones y si el cifrado del protocolo de transporte seguro en tiempo real (SRTP) es obligatorio.

Quién puede ejecutar este cmdlet: De forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **New-CsTrunkConfiguration** de manera local: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC), se ha asignado este cmdlet (incluidos los roles RBAC que haya creado usted mismo) para ejecutar el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrunkConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Requerido</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificador único que incluye el ámbito de la configuración troncal. La configuración troncal puede estar en el ámbito de sitio, o bien en el ámbito de servicio en el caso de un servicio de puerta de enlace RTC. (De forma predeterminada existe una configuración global, que no puede quitarse ni crearse de nuevo.) Por ejemplo, site:Redmond (para sitio) o PstnGateway:Redmond.litwareinc.com (para servicio).</p></td>
</tr>
<tr class="even">
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>El valor de este parámetro determina si existe un punto de terminación de medios conocido. (Un ejemplo de un punto de terminación de medios conocido sería una puerta de enlace RTC cuya terminación de medios tenga la misma IP que la terminación de señalización.) Si el tronco no tiene un punto de terminación de medios conocido, defina este valor en False.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Una cadena de caracteres que describe el propósito de la configuración troncal.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si se puede utilizar el protocolo 3pcc para permitir que las llamadas transferidas omitan el sitio alojado. 3pcc se denomina también &quot;control de terceros&quot;, y se produce cuando se utiliza a un tercero para conectar a dos autores de llamada (por ejemplo, un operador realiza una llamada de la persona A a la persona B). El método REFER es un método estándar de SIP que indica que el destinatario debe comunicarse con un tercero mediante la información proporcionada por el remitente. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBypass</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>El valor de este parámetro determina si la omisión de medios está habilitada para este tronco. Establezca este valor en True para habilitar la derivación. Tenga en cuenta que para que la omisión de medios funcione correctamente, las puertas de enlace RTC, los controladores SBC y los sistemas PBX deben ser compatibles con determinadas prestaciones, como:</p>
<p>- Recibir respuestas bifurcadas para una invitación (Invite).</p>
<p>- Los clientes de Lync Server y el punto de terminación de medios deben poder comunicarse directamente sin pasar por un Servidor de mediación.</p>
<p>- La subred de la puerta de enlace debe definirse en el mismo sitio que la subred del cliente o, si se encuentra en un sitio diferente, los sitios no deben separarse mediante vínculos WAN con un ancho de banda restringido.</p>
<p>La omisión de medios solo puede habilitarse en las siguientes circunstancias:</p>
<p>- El parámetro ConcentratedTopology está establecido en True</p>
<p>- El parámetro EnableReferSupport está establecido en False y los parámetros RTCPActiveCalls y RTCPCallsOnHold están establecidos en False, o EnableReferSupport está establecido en True</p>
<p>Tenga en cuenta que si EnableBypass está establecido en True y el valor de EnableReferSupport es False, las llamadas de omisión que se transfieran a continuación pasarán a ser de no omisión.</p>
<p>Para que la omisión de medios funcione correctamente para un elemento troncal concreto, debe habilitarse de forma global así como para el elemento en cuestión. Use el cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong> para habilitar la omisión de medios de forma global.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Cuando está establecido en True, las llamadas salientes que no son respondidas por la puerta de enlace dentro de los 10 segundos se reenviarán al siguiente tronco disponible; si no hay líneas troncales disponibles, se interrumpirá la llamada. En una organización con redes lentas y respuestas a las puertas de enlace, puede tener como resultado interrupciones innecesarias de las llamadas.</p>
<p>El valor predeterminado es True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Cuando está configurado como True, el enrutamiento de voz según ubicación estará habilitado para las llamadas que atraviesen los troncos SIP administrados por la recopilación especificada de opciones de configuración de troncos SIP. Con el enrutamiento de voz según ubicación, la ubicación del usuario que realiza la llamada y la del usuario que la recibe se tienen en cuenta a la hora de redirigir las llamadas. Si esta propiedad se configura como True (el valor predeterminado es False), se debe configurar también la propiedad NetworkSiteId.</p>
<p>Este parámetro se introdujo en la versión de febrero de 2013 de Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Define si el proveedor de servicios es un operador de telefonía móvil.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si los troncos SIP son compatibles con la voz en línea. Con la voz en línea, los usuarios tienen una cuenta de servidor Lync local, pero su correo de voz está alojado en Office 365. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Define si deben desviarse las llamadas de emergencia con PIDF-LO (Presence Information Data Format Location Object) a través de la puerta de enlace definida. Establezca este parámetro en True si las llamadas de emergencia deben desviarse a un proveedor de servicios de emergencia certificado. (La ubicación se transmitirá con la llamada.)</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Define si el tronco admite la recepción de solicitudes de referencia (Refer) del Servidor de mediación.</p>
<p>La omisión de medios solo puede habilitarse en las siguientes circunstancias:</p>
<p>- El parámetro ConcentratedTopology está establecido en True</p>
<p>- El parámetro EnableReferSupport está establecido en False y los parámetros RTCPActiveCalls y RTCPCallsOnHold están establecidos en False, o EnableReferSupport está establecido en True</p>
<p>Tenga en cuenta que si EnableBypass está establecido en True y el valor de EnableReferSupport es False, las llamadas de omisión que se transfieran a continuación pasarán a ser de no omisión.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si los troncos SIP admiten el cierre RTP. El cierre RTP es una tecnología que permite la conectividad RTP/RTCP a través de un firewall o dispositivo NAT (traductor de direcciones de red). El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Especifica si está habilitado el temporizador de la sesión. Los temporizadores de sesión se usan para determinar si una sesión determinada continúa activa.</p>
<p>Tenga en cuenta que aun cuando este parámetro esté establecido en False, pueden aplicarse temporizadores de sesión si la conexión remota tiene el temporizador de sesión habilitado. En tal caso, el Servidor de mediación responderá a las pruebas del temporizador de sesión desde la entidad remota.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Cuando este parámetro está establecido en True, la puerta de enlace RTC, el sistema IP-PBX o el controlador SBC del proveedor de servicios incrementarán el volumen de audio en las secuencias de voz que se envían a los clientes de Servidor de mediación o de Lync Server. Si este valor se establece en False, el audio también incrementará en el Servidor de mediación (para llamadas que no son de omisión) o en los clientes Lync Server (para llamadas de omisión).</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si la información del historial de llamadas se reenviará a través del tronco. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Indica si se reenviará el encabezado P-Asserted-Identity (PAI) junto con la llamada. El encabezado PAI permite comprobar la identidad del autor de la llamada. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Opcional</p></td>
<td><p>UInt32</p></td>
<td><p>El número máximo de respuestas bifurcadas que una puerta de enlace RTC, un sistema IP-PBX o el SBC del proveedor de servicios puede recibir para una invitación (Invite) enviada al Servidor de mediación.</p>
<p>Valor predeterminado: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Identificador de sitio del sitio de red asociado a la nueva recopilación de opciones de configuración de tronco. Si la propiedad EnableLocationRestriction está configurada como True, el enrutamiento de voz según ubicación a través de este tronco se administrará utilizando las opciones configuradas para el sitio especificado. Los identificadores de sitio de red se pueden recuperar mediante este comando:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p>
<p>Este parámetro se introdujo en la versión de febrero de 2013 de Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Colección de reglas de conversión de números de llamada saliente asignadas al tronco. Puede recuperar información acerca de las reglas disponibles ejecutando este comando:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una recopilación de reglas de conversión de números de teléfono que se aplican a las llamadas administradas por el enrutamiento saliente (llamadas enrutadas a destinos PBX o RTC).</p>
<p>A pesar de que la lista y las reglas pueden crearse directamente con este cmdlet, se recomienda crear las reglas de conversión saliente con el cmdlet <strong>New-CsOutboundTranslationRule</strong>, que crea la regla y la asigna a la configuración troncal que tenga el mismo ámbito.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Colección de usos de RTC asignados al tronco. Puede recuperar información acerca de los usos disponibles ejecutando este comando:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Al establecer este parámetro en True, el Servidor de mediación quitará los signos más (+) iniciales de los URI antes de enviarlos al proveedor de servicios.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Este parámetro determina si los paquetes RTCP se envían desde la puerta de enlace RTC, el sistema IP-PBX o el controlador SBC al proveedor de servicios para llamadas activas. En este contexto, una llamada activa es una llamada en la que se permite el flujo de medios como mínimo en una dirección. Si RTCPActiveCalls se establece en True, el cliente de Servidor de mediación o Lync Server puede finalizar una llamada si no recibe paquetes RTCP durante un período superior a los 30 segundos.</p>
<p>Tenga en cuenta que, si se deshabilitan las comprobaciones para los medios RTCP recibidos para las llamadas activas en los elementos de Lync Server, se quita una medida de seguridad importante para detectar si se ha descartado un dispositivo del mismo tipo; por consiguiente, solo deben deshabilitarse si es necesario.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Este parámetro determina si los paquetes RTCP siguen enviándose a través del tronco para llamadas que han estado retenidas y no se espera que fluyan paquetes de medios en ninguna dirección. Si Música en espera está habilitado en el tronco o el cliente de Lync Server, se considerará que la llamada está activa y esta propiedad se omitirá. En estas circunstancias, debe usarse el parámetro RTCPActiveCalls.</p>
<p>Tenga en cuenta que, si se deshabilitan las comprobaciones para los medios RTCP recibidos para las llamadas activas en los elementos de Lync Server, se quita una medida de seguridad importante para detectar si se ha descartado un dispositivo del mismo tipo; por consiguiente, solo deben deshabilitarse si es necesario.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de reglas de conversión de códigos de respuesta SIP que se aplican a los códigos de respuesta recibidos de una puerta de enlace RTC, un sistema IP-PBX o un controlador SBC en el proveedor de servicios. Estas reglas permiten al administrador asignar códigos de respuesta SIP con valores entre 400 y 699 recibidos a través de un tronco a nuevos valores más coherentes con Lync Server.</p>
<p>Esta lista y las reglas correspondientes pueden crearse directamente con este cmdlet. No obstante, se recomienda crear las reglas de conversión de códigos de respuesta SIP llamando al cmdlet <strong>New-CsSipResponseCodeTranslationRule</strong>. Dicho cmdlet creará la regla y la asignará a la configuración troncal con el ámbito correspondiente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Opcional</p></td>
<td><p>SRTPMode</p></td>
<td><p>El valor de este parámetro determina el nivel de compatibilidad de SRTP para proteger el tráfico multimedia entre el Servidor de mediación y la puerta de enlace RTC, el sistema IP-PBX o el controlador SBC en el proveedor de servicios. En los casos de omisión de medios, este valor debe ser compatible con el valor de EncryptionLevel en la configuración de medios. La configuración de medios se define mediante los cmdlets <strong>New-CsMediaConfiguration</strong> y <strong>Set-CsMediaConfiguration</strong>.</p>
<p>Valores válidos:</p>
<p>- Required: debe usarse el cifrado SRTP.</p>
<p>- Optional: se usará el cifrado SRTP si la puerta de enlace lo admite.</p>
<p>- NotSupported: el cifrado SRTP no está admitido y, por tanto, no se usará.</p>
<p>Nota: SRTPMode solo se utiliza si la puerta de enlace está configurada para usar TLS (Seguridad de la capa de transporte). Si la puerta de enlace está configurada con TCP (Protocolo de control de transmisión) como transporte, SRTPMode se establece internamente en NotSupported.</p>
<p>Valor predeterminado: Requerido</p></td>
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

Ninguno.

## Tipos de valores devueltos

Crea un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Vea también

#### Otros recursos

[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)

