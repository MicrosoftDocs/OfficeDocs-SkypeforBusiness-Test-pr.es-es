---
title: New-CsVoicePolicy
TOCTitle: New-CsVoicePolicy
ms:assetid: 3852de89-a604-437a-9fdf-3597b88ce13d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg425856(v=OCS.15)
ms:contentKeyID: 48274927
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicePolicy

 

_**Última modificación del tema:** 2015-03-09_

Crea una directiva de voz. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsVoicePolicy -Identity <XdsIdentity> [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## EJEMPLO 1

En este ejemplo se crea una directiva de voz por usuario (con los valores predeterminados) y cuyo parámetro Identity es UserVoicePolicy1.

    New-CsVoicePolicy -Identity UserVoicePolicy1

## EJEMPLO 2

En este ejemplo se crea una directiva de voz por usuario con una Identity de UserVoicePolicy2 y se establece la propiedad AllowSimulRing en False, lo que quiere decir que los usuarios que tengan asignada esta directiva no pueden usar las llamadas simultáneas, una característica que determina si se puede establecer un segundo teléfono (como un teléfono móvil) para que suene cada vez que el teléfono de la oficina del usuario reciba una llamada. Este comando también agrega "Local" a la lista de usos de RTC, lo que asocia esta directiva de voz con una ruta de voz que también utiliza el uso de RTC local. (Tenga en cuenta que el parámetro Identity no está especificado de forma explícita. El parámetro Identity es un parámetro de posición; por lo tanto, si coloca el valor de identidad al principio de la lista de parámetros, no es necesario que indique de forma explícita que se trata del valor de Identity.)

    New-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{add = "Local"}

## EJEMPLO 3

En este ejemplo se crea una directiva de voz para el sitio Redmond y se aplican a ella todos los usos de RTC definidos para la organización. La primera línea del ejemplo llama al cmdlet **Get-CsPstnUsage** para recuperar el conjunto global de usos de RTC de la organización, y guardarlo en la variable $a. La segunda línea llama al cmdlet **New-CsVoicePolicy** con el objetivo de crear una nueva directiva de voz para el sitio Redmond. Para agregar a esta directiva la lista que incluye el conjunto global de usos de RTC, se transfiere un valor al parámetro PstnUsages. Observe la sintaxis del valor de adición: $a.Usage. Hace referencia a la propiedad Usage de la configuración de uso de RTC, que contiene la lista de usos de RTC.

    $a = Get-CsPstnUsage
    New-CsVoicePolicy site:Redmond -PstnUsages @{add = $a.Usage}

## Descripción detallada

Este cmdlet crea una directiva de voz. Las directivas de voz se usan para administrar características de Telefonía IP empresarial, como las llamadas simultáneas (la posibilidad de recibir una segunda llamada cada vez que alguien llama al número de una oficina) o el desvío de llamadas. La directiva creada mediante este cmdlet determina si muchas de estas características están habilitadas o deshabilitadas.

Quién puede ejecutar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos tienen autorización para ejecutar el cmdlet **New-CsVoicePolicy** localmente: RTCUniversalServerAdmins. Para obtener una lista de todos los roles de control de acceso basado en rol (RBAC), este rol se ha asignado (así como cualquier otro rol RBAC personalizado que haya creado) para ejecutar el siguiente comando desde el símbolo del sistema Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicePolicy"}

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
<td><p>Identificador único que especifica el ámbito o el nombre de la directiva. Los valores válidos para este cmdlet son site:&lt;nombre del sitio&gt; (donde &lt;nombre del sitio&gt; es el nombre del sitio de Lync Server al que se aplica esta directiva, por ejemplo, site:Redmond) y una cadena que designa una directiva por usuario, por ejemplo, RedmondVoicePolicy. Existe una directiva global de manera predeterminada.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Si este parámetro está establecido en True, las llamadas pueden desviarse. Si está definido en False, las llamadas no pueden desviarse.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Si este parámetro está establecido en True, las llamadas a números internos de otro grupo de servidores se enrutarán a través de la red telefónica conmutada pública si el grupo de servidores o red WAN no está disponible.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Las llamadas simultáneas son una característica que permite que varios teléfonos reciban una misma llamada al marcar un solo número. Al definir este parámetro en True, se habilita esta característica. Si el parámetro está establecido en False, no se podrán configurar llamadas simultáneas para ningún usuario que esté asignado a esta directiva.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Opcional</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Proporciona un modo de que los administradores gestionen el desvío de llamadas y las llamadas simultáneas. Los valores permitidos son:</p>
<p>* VoicePolicyUsage: el uso de la directiva de voz predeterminado se destina a administrar el desvío de llamadas y las llamadas simultáneas en todos los casos. Es el valor predeterminado.</p>
<p>* InternalOnly: el desvío de llamadas y las llamadas simultáneas se limitan a las llamadas realizadas de un usuario de Lync a otro.</p>
<p>* CustomUsage. Se aplicará un uso de RTC personalizado para administrar el desvío de llamadas y las llamadas simultáneas. Este uso debe especificarse con el parámetro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Uso de RTC personalizado que se aplica para administrar el desvío de llamadas y las llamadas simultáneas. Para agregar un uso personalizado a la directiva de voz, use una sintaxis similar a esta:</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Para quitar un uso personalizado, use esta sintaxis:</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Tenga en cuenta que el uso debe existir antes de que se pueda usar con el parámetro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Una descripción de la directiva de voz.</p>
<p>Longitud máxima: 1040 caracteres.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Las directivas se pueden definir para administrar la configuración de red, incluida la limitación del ancho de banda. Al definir este parámetro en True, se permite la invalidación de las directivas. Es decir, si es True, no se realizarán comprobaciones de ancho de banda y las llamadas se realizarán al margen de la configuración de control de admisión de llamadas (CAC).</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>La aplicación Aplicación de estacionamiento de llamadas permite retener o estacionar una llamada de un número determinado de un intervalo de números para recuperarla más tarde. Al definir este parámetro en True, se habilita esta aplicación. Si está definido en False, los usuarios que estén asignados a esta directiva no podrán estacionar llamadas que se hayan marcado para su número de teléfono.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Determina si las llamadas se pueden transferir a otro número. Si este parámetro está definido en True, las llamadas pueden transferirse; si está definido en False, las llamadas no pueden transferirse.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>La delegación de llamadas permite a un usuario responder a las llamadas por otro usuario o realizar llamadas en nombre de otro usuario. Por ejemplo, un coordinador puede configurar la delegación de llamadas para que tanto su teléfono como el de un administrador reciban todas las llamadas entrantes. Al definir este parámetro en True, los usuarios con esta directiva pueden definir la delegación de llamadas. Al definir este parámetro en False, se deshabilita la delegación de llamadas.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>La grabación de llamadas malintencionadas es una opción estándar que se proporciona para grabar las llamadas que un usuario designe como malintencionadas. Las llamadas se pueden grabar aunque el ID del autor de la llamada esté bloqueado. La grabación solo está disponible para las autoridades apropiadas y, en ningún caso, para el usuario. Al definir esta propiedad en True, se habilita la posibilidad de establecer una grabación en las llamadas malintencionadas.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>La llamada de equipo permite a un usuario designar un grupo de usuarios cuyos teléfonos sonarán cuando el número del usuario reciba una llamada. Esta característica es útil en los equipos donde, por ejemplo, cualquiera de los miembros del equipo puede responder a las llamadas entrantes de clientes. Al definir este parámetro en True, se habilita esta característica.</p>
<p>Valor predeterminado: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Cuando se establece en True, las llamadas realizadas a un dispositivo móvil sin respuesta se enrutarán al correo de voz de la organización en vez del correo de voz del proveedor del dispositivo móvil. Si se contesta una llamada &quot;demasiado pronto&quot; (es decir, antes de que haya pasado el valor configurado para la propiedad PSTNVoicemailEscapeTimer), se dará por supuesto que el dispositivo móvil no está disponible y se enrutará la llamada al correo de voz de la organización.</p>
<p>El valor predeterminado es False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime las preguntas de confirmación que aparecerían antes de realizar cambios.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Opcional</p></td>
<td><p>String</p></td>
<td><p>Un nombre para mostrar que identifica a esta directiva.</p>
<p>Valor predeterminado: DefaultPolicy</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Opcional</p></td>
<td><p>Boolean</p></td>
<td><p>Las tarifas RTC se conocen más habitualmente como tarifas de larga distancia. En algunas ocasiones, las organizaciones pueden omitir estas tarifas mediante la implementación de una solución de voz sobre IP (VoIP), que permite a las sucursales conectarse mediante llamadas en red. Al definir este parámetro en True, las llamadas se enviarán a través de la RTC y se incurrirá en gastos, en lugar de establecer la conexión a través de la red y omitir las tarifas.</p>
<p>Valor predeterminado: False</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de usos de RTC disponibles para esta directiva. El uso de RTC vincula una directiva de voz con una ruta telefónica.</p>
<p>Puede poner cualquier valor de cadena en esta lista siempre que dicho valor esté incluido en la lista global actual de usos de RTC. (No están permitidas las cadenas duplicadas. Todas las cadenas deben ser únicas.) La lista de usos de RTC se puede recuperar mediante una llamada al cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>De forma predeterminada, esta lista está vacía. Si no proporciona un valor para este parámetro, recibirá un mensaje de advertencia donde se indicará que los usuarios a los que se otorgue esta directiva no podrán realizar llamadas RTC salientes.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int64</p></td>
<td><p>Tiempo necesario (en milisegundos) para determinar si una llamada se ha contestado &quot;demasiado pronto&quot;. Si se recibe una respuesta en este intervalo de tiempo, Lync Server dará por supuesto que el dispositivo móvil no está disponible y cambiará automáticamente la llamada al correo de voz de la organización. Si no hay respuesta antes de que transcurra el intervalo especificado, se permitirá que continúe la llamada. El valor predeterminado es de 1.500 milisegundos.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino de Skype Empresarial Online para la que se está creando la nueva directiva de voz. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Puede devolver el Id. de inquilino de cada uno de sus inquilinos ejecutando este comando:</p>
<p>Get-CsTenant | Select-Object Nombre para mostrar, Id. de inquilino</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceDeploymentMode</em></p></td>
<td><p>Opcional</p></td>
<td><p>VoiceDeploymentMode</p></td>
<td><p>Los valores permitidos son:</p>
<p>* OnPrem</p>
<p>* Online</p>
<p>* OnlineBasic</p>
<p>* OnPremOnlineHybrid</p>
<p>El valor predeterminado es OnPrem.</p></td>
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

Este cmdlet crea una instancia del objeto Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy.

## Vea también

#### Otros recursos

[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

