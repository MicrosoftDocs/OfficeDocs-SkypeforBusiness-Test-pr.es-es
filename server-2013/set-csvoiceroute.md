---
title: Set-CsVoiceRoute
TOCTitle: Set-CsVoiceRoute
ms:assetid: b786aec0-946e-4ce5-812e-25e5d8cfa4d5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412893(v=OCS.15)
ms:contentKeyID: 48276437
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoute

 

_**Última modificación del tema:** 2015-03-09_

Modifica una ruta de voz. Las rutas de voz contienen instrucciones que indican a Lync Server cómo enrutar las llamadas de usuarios de telefonía IP empresarial al número de teléfono de la red telefónica conmutada (RTC) o a una central de conmutación PBX. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

Este comando establece la descripción de la ruta de voz Route1 en "Test Route".

    Set-CsVoiceRoute -Identity Route1 -Description "Test Route"

## Ejemplo 2

El comando de este ejemplo modifica la ruta de voz con la identidad Route1 para agregar el uso de PSTN Long Distance a la lista de usos para esta ruta de voz. Long Distance debe estar en la lista de usos de RTC globales (que puede recuperarse llamando al cmdlet **Get-CsPstnUsage**).

    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"}

## Ejemplo 3

En este ejemplo se modifica la ruta de voz denominada Route1 para rellenar la lista de usos de RTC de dicha ruta con todos los usos existentes para la organización. El primer comando de este ejemplo recupera la lista de usos de teléfono RTC globales. Tenga en cuenta que la llamada al cmdlet **Get-CsPstnUsage** se encuentra entre paréntesis, lo que significa que primero se recupera un objeto que contiene la información de uso de RTC. (Como solo hay un uso de RTC global, se recuperará un único objeto). A continuación, el comando recupera la propiedad Usage del objeto. Dicha propiedad, que contiene una lista de usos de RTC, se asigna a la variable $x. En la segunda línea de este ejemplo, se llama al cmdlet **Set-CsVoiceRoute** para modificar la ruta de voz con la identidad Route1. Preste atención al valor enviado al parámetro PstnUsages: @{replace=$x}. Este valor indica que se debe reemplazar todo el contenido de la lista PstnUsages de esta ruta por el contenido de $x, que contiene la lista de usos RTC recuperada en la línea 1.

    $x = (Get-CsPstnUsage).Usage
    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{replace=$x}

## Ejemplo 4

Este conjunto de comandos cambia la propiedad Name de la ruta de voz de la identidad Route1 a RouteA. Al cambiar la propiedad Name, se cambia automáticamente la propiedad Identity, en este caso a RouteA.

En la primera línea, se llama al cmdlet **Get-CsVoiceRoute** para recuperar la ruta de voz con la identidad Route1. El objeto devuelto se almacena en la variable $x. A continuación, la propiedad Name del objeto se asigna al valor de cadena "RouteA". Por último, el objeto (contenido en la variable $x) se envía al parámetro Instance del cmdlet **Set-CsVoiceRoute** para realizar el cambio.

    $x = Get-CsVoiceRoute -Identity Route1
    $x.Name = "RouteA"
    Set-CsVoiceRoute -Instance $x

## Ejemplo 5

En este ejemplo se modifica la ruta de voz denominada Route1 y se rellena la lista de puertas de enlace RTC (PstnGatewayList) de la ruta con el rol de servidor de la puerta de enlace con la identidad PstnGateway:192.168.0.100. En la primera línea de este ejemplo, se llama al cmdlet **Get-CsVoiceRoute** para recuperar la ruta de voz que se desea modificar, en este caso Route1. A continuación, se llama al método Add en la propiedad PstnGatewayList de Route1. Enviamos la identidad del servicio que queremos agregar al método Add. Por último, llamamos al cmdlet **Set-CsVoiceRoute**, y enviamos la variable $y al parámetro Instance, con lo que se actualizará la identidad Route1 (almacenada en $y) con la puerta de enlace RTC recién agregada.

    $y = Get-CsVoiceRoute -Identity Route1
    $y.PstnGatewayList.Add("PstnGateway:192.168.0.100")
    Set-CsVoiceRoute -Instance $y

## Descripción detallada

Use este cmdlet para modificar una ruta de voz existente. Las rutas de voz se asocian a las directivas de voz con los usos de red telefónica conmutada (RTC). Una ruta de voz incluye una expresión regular que identifica qué números de teléfono se enrutarán a través de una ruta de voz determinada: los números de teléfono que coincidan con la expresión regular se enrutarán a través de esta ruta.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **Set-CsVoiceRoute** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoute"}

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
<td><p><em>AlternateCallerId</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Si el parámetro SuppressCallerId se define en True, se mostrará a las partes receptoras el valor de parámetro AlternateCallerId, en lugar del número real del autor de la llamada. Este número debe ser un número válido y se puede usar para representar un departamento de una organización, como Soporte Técnico o Recursos Humanos.</p>
<p>Si el parámetro SuppressCallerId se establece en False, se ignorará el parámetro AlternateCallerId.</p>
<p>Este valor debe tener el mismo formato que la expresión regular (\+)?[1-9]\d*(;ext=[1-9]\d*)?. En otras palabras, el valor puede comenzar por un signo más (+), pero no es necesario; puede contener cualquier cantidad de dígitos y puede ir seguido de una extensión que empiece con ;ext=, seguida de un número cualquiera de dígitos. (Tenga en cuenta que si incluye una extensión, la cadena de caracteres debe delimitarse entre comillas dobles).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Descripción de la utilidad de la ruta de teléfono.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>La identidad única de la ruta de voz. (Si el nombre de la ruta contiene un espacio, como Test Route, deberá delimitar la cadena de caracteres completa entre paréntesis).</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>Ruta</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes. Este objeto debe ser de tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route y puede recuperarse llamando al cmdlet <strong>Get-CsVoiceRoute</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberPattern</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Una expresión regular que especifica los números de teléfono a los que se aplica esta ruta. Los números que coincidan con este patrón se enrutarán de acuerdo con el resto de la configuración de enrutamiento. Por ejemplo, el patrón numérico predeterminado, [0-9]{10}, especifica un número de 10 dígitos que contiene cualquier dígito del 0 al 9.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Int32</p></td>
<td><p>Un número podría resultar en varias rutas de voz. La prioridad determina el orden en que se aplicarán las rutas, en caso de que sea posible más de una ruta.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un Servidor de mediación puede asociarse con varias puertas de enlace. Este parámetro contiene una lista de puertas de enlace asociadas a esta ruta de voz. Todos los miembros de la lista deben tener la identidad de servicio de la puerta de enlace RTC o el Servidor de mediación. El valor puede hacer referencia a un Servidor de mediación solamente si el Servidor de mediación está configurado para Microsoft Office Communications Server 2007 o Microsoft Office Communications Server 2007 R2. Para Lync Server, se puede emplear una puerta de enlace RTC. La identidad de servicio es una cadena de caracteres con el formato ServiceRole:FQDN, donde ServiceRole es el nombre del rol de servicio (PSTNGateway) y FQDN es el nombre de dominio completo (FQDN) del grupo de servidores o la dirección IP del servidor. Por ejemplo, PSTNGateway:redmondpool.litwareinc.com. Las identidades de servicio se pueden recuperar llamando al comando Get-CsService | identidad Select-Object.</p>
<p>Si realiza cambios en una ruta de voz y deja vacía la lista PstnGatewayList, o bien si el cambio que realiza quita todos los elementos de la lista, recibirá un mensaje de advertencia conforme que ningún usuario podrá realizar llamadas de RTC.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Una lista de usos de RTC, como Local o Long Distance, que se pueden aplicar a la ruta de voz. El uso de RTC debe ser un uso existente. (Los usos de RTC pueden recuperarse llamando al cmdlet <strong>Get-CsPstnUsage</strong>).</p>
<p>Si realiza cambios en una ruta de voz y deja vacía la lista PstnUsages, o bien si el cambio que realiza quita todos los usos de RTC de la lista, recibirá un mensaje de advertencia conforme que ningún usuario podrá realizar llamadas de RTC.</p></td>
</tr>
<tr class="odd">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Determina si el ID del autor de la llamada se mostrará en las llamadas salientes. Si este parámetro se define en True, se suprimirá el ID del autor de la llamada. En lugar del ID real, se mostrará el valor de AlternateCallerId. Si SuppressCallerId se define en True, debe indicarse un valor para AlternateCallerId.</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route. El cmdlet **Set-CsVoiceRoute** acepta la entrada canalizada de objetos de ruta de voz.

## Tipos de valores devueltos

El cmdlet **Set-CsVoiceRoute** no devuelve ningún valor u objeto. Por el contrario, el cmdlet configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Vea también

#### Otros recursos

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)

