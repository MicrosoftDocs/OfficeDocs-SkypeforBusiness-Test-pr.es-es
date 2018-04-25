---
title: Set-CsTrunkConfiguration
TOCTitle: Set-CsTrunkConfiguration
ms:assetid: 18152388-68de-4a6b-b5a1-248534ecde72
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg398238(v=OCS.15)
ms:contentKeyID: 48274565
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrunkConfiguration

 

_**Última modificación del tema:** 2015-02-27_

Modifica una configuración del tronco existente que describe la configuración de una entidad del mismo nivel de tronco, como una puerta de enlace de red telefónica conmutada (RTC), una central de conmutación (PBX) de IP pública o un controlador de borde de sesión (SBC) del proveedor de servicios. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTrunkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo se modifica una configuración del tronco con el valor de Identity site:Redmond para habilitar la derivación de medios. La derivación de medios se habilita al asignar el valor $True al parámetro EnableBypass. El resto de las propiedades de esta configuración conservará sus valores existentes.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## EJEMPLO 2

En este ejemplo se modifica una regla de conversión de salida definida para la configuración del tronco con la identidad site:Redmond. Observe que, en realidad, no realizamos ninguna llamada al cmdlet **Set-CsTrunkConfiguration** para efectuar este cambio. Los cambios realizados con el cmdlet **Set-CsOutboundTranslationRule** se reflejarán automáticamente en la configuración del tronco con una identidad que coincida con la parte del ámbito de la identidad de la regla de conversión de salida.

    Set-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Translation '$1'

## EJEMPLO 3

En el ejemplo 3 se establece SRTPMode para todas las configuraciones del tronco en el ámbito del sitio en Optional. La primera parte del comando es una llamada al cmdlet **Get-CsTrunkConfiguration** que usa el parámetro Filter para recuperar todas las configuraciones del tronco cuyo Identity comienza por site:, es decir, todas las configuraciones del tronco definidas en el nivel de sitio. A continuación, esta colección de configuraciones se transfiere al cmdlet **Set-CsTrunkConfiguration**, que establece la propiedad SRTPMode de cada una de ellas en Optional.

    Get-CsTrunkConfiguration -Filter site:* | Set-CsTrunkConfiguration -SRTPMode "Optional"

## EJEMPLO 4

En el ejemplo 4 se modifica una configuración del tronco con el valor de Identity site:Redmond para habilitar la compatibilidad de PIDF-LO. De forma predeterminada, el parámetro EnablePIDFLOSupport es False. En este ejemplo, el valor se estableció en True para habilitar una ubicación compatible con llamadas de emergencia. Debe establecer EnablePIDFLOSupport en True para que la información de ubicación pueda ser enviada al tronco por la aplicación de enrutamiento de salida.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnablePIDFLOSupport $True

## Descripción detallada

Use este cmdlet para modificar una configuración del tronco aplicable a entidades de puerta de enlace RTC. Cada configuración consta de opciones específicas para una entidad del mismo nivel de tronco, como una puerta de enlace RTC, IP-PBX o SBC del proveedor de servicios. Esta configuración establece aspectos, por ejemplo, si la omisión de medios está habilitada en este tronco, si los paquetes del protocolo de transporte en tiempo real (RTCP) se envían bajo determinadas condiciones y si el cifrado del protocolo de transporte seguro en tiempo real (SRTP) es obligatorio.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **Set-CsTrunkConfiguration** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrunkConfiguration"}

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
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>El valor de este parámetro determina si hay un punto de terminación de medios conocido. (Un ejemplo de un punto de terminación de medios conocido sería una puerta de enlace RTC cuya terminación de medios tenga la misma IP que la terminación de señalización.) Establezca este valor en False si el tronco no tiene un punto de terminación de medios conocido.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Una cadena que describe el objetivo de la configuración del tronco.</p></td>
</tr>
<tr class="even">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Indica si el protocolo 3pcc se puede usar para permitir que las llamadas transferidas prescindan del sitio hospedado. 3pcc también se conoce como &quot;control de terceros&quot; y se produce cuando se usa un tercero para conectar un par de autores de llamada (por ejemplo, un operador que hace una llamada de la persona A a la persona B). El método REFER es un método SIP estándar que indica que el destinatario debería ponerse en contacto con un tercero mediante la información que proporciona el remitente. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBypass</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>El valor de este parámetro determina si hay habilitado una derivación de medios para este tronco. Establezca este valor en True para habilitar la derivación. Tenga en cuenta que, para que la derivación de medios funcione correctamente, las puertas de enlace RTC, los SBC y las PBX deben dar cabida a una serie de funciones, como:</p>
<p>- La capacidad de recibir respuestas bifurcadas para Invitar.</p>
<p>- Los clientes de Lync Server y el punto de terminación de medios deben poder comunicarse directamente sin pasar por un Servidor de mediación.</p>
<p>- La subred de la puerta de enlace debe estar definida como perteneciente al mismo sitio que la subred del cliente, o bien, si está en un sitio diferente, los sitios no deberán estar separados mediante vínculos WAN con un ancho de banda restringido.</p>
<p>La desviación de medios se puede habilitar únicamente bajo las siguientes circunstancias:</p>
<p>- El parámetro ConcentratedTopology está establecido en True</p>
<p>- El parámetro EnableReferSupport está establecido en False y RTCPActiveCalls y RTCPCallsOnHold, en False, o bien EnableReferSupport está establecido en True</p>
<p>Tenga en cuenta que si EnableBypass es True y EnableReferSupport, False, las llamadas de desvío que se transfieran posteriormente se convertirán en llamadas de no derivación.</p>
<p>Para que la desviación de medios funcione correctamente con un tronco en particular, debe habilitarse globalmente, y también para el tronco en cuestión. Use el cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong> para habilitar la desviación de medios de forma global.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Cuando se establece en True, las llamadas salientes que no son respondidas por la puerta de enlace dentro de los 10 segundos se reenviarán al siguiente troncal disponible; si no hay líneas troncales disponibles, se interrumpirá la llamada. En una organización con redes lentas y respuestas a las puertas de enlace, puede tener como resultado interrupciones innecesarias de las llamadas.</p>
<p>El valor predeterminado es True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Cuando se establece en True, el enrutamiento de voz basado en ubicación se habilitará para las llamadas que pasan a través de los troncos SIP administrados por la colección especificada de opciones de configuración de tronco SIP. Con el enrutamiento de voz basado en ubicación, al enrutar las llamadas se tienen en cuenta las ubicaciones tanto del usuario que realiza la llamada como del usuario que la recibe. Si esta propiedad se establece en True (el valor predeterminado es False), también se debe establecer la propiedad NetworkSiteId.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Define si el proveedor de servicios es un operador de telefonía móvil.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Indica si los troncos SIP son compatibles con la voz en línea. Con la voz en línea, los usuarios tienen una cuenta de Lync Server local, pero su correo de voz se hospeda en Skype Empresarial Online. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Establece si las llamadas de emergencia se van a enrutar con un objeto PIDF-LO a través de la puerta de enlace definida. Establezca este parámetro en True si las llamadas de emergencia se van a enrutar a un proveedor de servicios de emergencia certificado (la ubicación se transmitirá con la llamada).</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Define si el tronco admite la recepción de solicitudes de referencia del Servidor de mediación.</p>
<p>La desviación de medios se puede habilitar únicamente bajo las siguientes circunstancias:</p>
<p>- El parámetro ConcentratedTopology está establecido en True</p>
<p>- El parámetro EnableReferSupport está establecido en False y RTCPActiveCalls y RTCPCallsOnHold, en False, o bien EnableReferSupport está establecido en True</p>
<p>Tenga en cuenta que si EnableBypass es True y EnableReferSupport, False, las llamadas de desvío que se transfieran posteriormente se convertirán en llamadas de no derivación.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Indica si los troncos SIP admiten el cierre de RTP. El cierre de RTP es una tecnología que permite la conectividad RTP/RTCP a través de un dispositivo o firewall de NAT (traductor de direcciones de red). El valor predeterminado es False ($False)</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Especifica si se ha habilitado el temporizador de sesión. Los temporizadores de sesión se utilizan para determinar si una sesión determinada aún está activa.</p>
<p>Recuerde que, aun cuando este parámetro sea False, los temporizadores de sesión serán aplicables si la conexión remota tiene el temporizador de sesión habilitado, en cuyo caso el Servidor de mediación responderá a las pesquisas del temporizador de sesión desde la entidad remota.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Cuando este parámetro se establece en True, la puerta de enlace RTC, IP-PBX o SBC en el proveedor de servicios aumentará el volumen de audio en las secuencias de voz que se envían al Servidor de mediación o los clientes de Lync Server. Si se establece en False, el audio aumentará en el Servidor de mediación (llamadas que no son de desvío) o bien en los clientes de Lync Server (llamadas de desvío).</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Indica si se reenviará información del historial de llamadas a través del tronco. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Indica si se reenviará el encabezado de identidad afirmada P (PAI) junto con la llamada. El encabezado PAI proporciona una forma de verificar la identidad del autor de la llamada. El valor predeterminado es False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificador único que incluye el ámbito de la configuración del tronco. Las configuraciones de tronco pueden estar en el ámbito global o de sitio, o bien en el ámbito de servicio en el caso de un servicio de puerta de enlace RTC. Por ejemplo, site:Redmond (ámbito del sitio) o PstnGateway:Redmond.litwareinc.com (ámbito del servicio).</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>TrunkConfiguration</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes.</p>
<p>Este parámetro precisa de un objeto de tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration, que se puede obtener si se llama al cmdlet <strong>Get-CsTrunkConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Opcional</p></td>
<td><p>UInt32</p></td>
<td><p>Número máximo de respuestas bifurcadas que una puerta de enlace RTC, IP-PBX o SBC del proveedor de servicios puede recibir para una invitación enviada al Servidor de mediación.</p>
<p>Valor predeterminado: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Identificador de sitio del sitio de red asociados con la colección de opciones de configuración de tronco. Si la propiedad EnableLocationRestriction se establece en True, el enrutamiento de voz basado en ubicación a través de este tronco se administrará con la configuración establecida para el sitio especificado. Los identificadores de sitio de red se pueden recuperar con este comando:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Colección de reglas de conversión salientes del número que llama asignadas al tronco. Para recuperar información acerca de las reglas disponibles, ejecute este comando:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una colección de reglas de traducción de números de teléfono que se aplica a las llamadas administradas mediante enrutamiento saliente (llamadas enrutadas a destinos PBX o RTC).</p>
<p>A pesar de que esta lista y estas reglas se pueden modificar directamente con este cmdlet, se recomienda usar el cmdlet <strong>Set-CsOutboundTranslationRule</strong> para modificar las reglas de conversión de salida. El cmdlet <strong>Set-CsOutboundTranslationRule</strong> modificará la regla y las modificaciones se reflejarán automáticamente en la configuración del tronco. Para modificar la configuración del tronco agregando una nueva regla de conversión de salida, llame al cmdlet <strong>New-CsOutboundTranslationRule</strong>. La nueva regla se agregará a la configuración del tronco cuyo ámbito coincida.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Colección de usos de RTC asignados al tronco. Para recuperar información acerca de los usos disponibles, ejecute este comando:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Al establecer este parámetro en True, el Servidor de mediación quitará los signos más (+) iniciales de los URI antes de enviarlos al proveedor de servicios.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Este parámetro determina si, en las llamadas activas, los paquetes RTCP se envían desde la puerta de enlace RTC, IP-PBX o SBC en el proveedor de servicios. En este contexto, una llamada activa consiste en una llamada donde los medios pueden fluir en al menos una dirección. Si RTCPActiveCalls se establece en True, el Servidor de mediación o el cliente de Lync Server podrán finalizar una llamada si no se reciben paquetes RTCP en un período de 30 segundos.</p>
<p>Tenga en cuenta que, si deshabilita las comprobaciones de los medios RTCP recibidos para las llamadas activas en los elementos de Lync Server, estará prescindiendo de un importante método para detectar pares descartados, por lo que se aconseja llevar esto a cabo únicamente cuando sea absolutamente necesario.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Este parámetro determina si los paquetes RTCP se continúan enviando a través del tronco para las llamadas puestas en espera y no se espera el paso de paquetes de medios en ninguna de las direcciones. Si Music on Hold está habilitado en el cliente de Lync Server o en el tronco, se considerará que la llamada está activa y esta propiedad se omitirá. En este tipo de situaciones, use el parámetro RTCPActiveCalls.</p>
<p>Tenga en cuenta que, si deshabilita las comprobaciones de los medios RTCP recibidos para las llamadas activas en los elementos de Lync Server, estará prescindiendo de un importante método para detectar pares descartados, por lo que se aconseja llevar esto a cabo únicamente cuando sea absolutamente necesario.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Lista de reglas de traducción de códigos de respuesta SIP que se aplican a los códigos de respuesta recibidos de una puerta de enlace RTC, IP-PBX o SBC en el proveedor de servicios. Mediante estas reglas, el administrador puede asignar códigos de respuesta SIP con valores entre 400 y 699 recibidos a través de un tronco a nuevos valores más uniformes con Lync Server.</p>
<p>Tanto la lista como las reglas correspondientes se pueden crear directamente con este cmdlet, si bien recomendamos crear las reglas de traducción de códigos de respuesta SIP llamando al cmdlet <strong>New-CsSipResponseCodeTranslationRule</strong>. Con él, se creará la regla y se asignará a la configuración del tronco cuyo ámbito coincida.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Opcional</p></td>
<td><p>SRTPMode</p></td>
<td><p>El valor de este parámetro determina el nivel de compatibilidad de SRTP para proteger el tráfico de medios entre el Servidor de mediación y la puerta de enlace RTC, IP-PBX o SBC en el proveedor de servicios. En los casos de desviación de medios, este valor debe ser compatible con el valor de EncryptionLevel en la configuración de medios. La configuración de medios se define mediante los cmdlets <strong>New-CsMediaConfiguration</strong> y <strong>Set-CsMediaConfiguration</strong>.</p>
<p>Valores válidos:</p>
<p>- Required: se debe usar el cifrado SRTP.</p>
<p>- Optional: se utilizará SRTP si el proveedor de servicios lo admite.</p>
<p>- NotSupported: el cifrado SRTP no se admite y, por lo tanto, no se usará.</p>
<p>Nota: SRTPMode solo se usa en caso de que la puerta de enlace se configure para usar la Seguridad de la capa de transporte (TLS). Si está configurada con el Protocolo de control de transmisión (TCP) como transporte, SRTPMode se establece internamente en NotSupported.</p>
<p>Valor predeterminado: Obligatorio</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration. Acepta entradas canalizadas de objetos de configuración de tronco.

## Tipos de valores devueltos

Este cmdlet no devuelve un valor, sino que modifica un objeto del tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Vea también

#### Otros recursos

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

