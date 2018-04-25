---
title: Set-CsVoicePolicy
TOCTitle: Set-CsVoicePolicy
ms:assetid: e6035b74-d760-4c48-aa0b-d09d129e0830
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399021(v=OCS.15)
ms:contentKeyID: 48276985
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicePolicy

 

_**Última modificación del tema:** 2015-03-09_

Modifica una directiva de voz existente. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Set-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

En este ejemplo se define la propiedad AllowSimulRing en False para la directiva por usuario UserVoicePolicy2, lo que quiere decir que los usuarios que tengan asignada esta directiva no pueden usar las llamadas simultáneas, una característica que determina si se puede establecer un segundo teléfono (como un teléfono móvil) para que suene cada vez que el teléfono de la oficina del usuario reciba una llamada. Este comando también quita la cadena de caracteres "Local" de la lista de usos de RTC para esta directiva. (Tenga en cuenta que el parámetro Identity no está especificado de forma explícita. El parámetro Identity es un parámetro de posición; por lo tanto, si coloca el valor de identidad al principio de la lista de parámetros, no es necesario que indique de forma explícita que se trata del valor de Identity.)

    Set-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{remove="Local"}

## Ejemplo 2

En este ejemplo, se modifica la directiva de voz del sitio Redmond de modo que se apliquen a la directiva todos los usos de RTC definidos en la organización. En la primera línea del ejemplo, se llama al cmdlet **Get-CsPstnUsage** para recuperar el conjunto global de usos de RTC de la organización y guardarlo en la variable $a. En la segunda línea, se llama al cmdlet **Set-CsVoicePolicy** para modificar la directiva de voz del sitio Redmond. Se transfiere un valor al parámetro PstnUsages para reemplazar la lista actual de usos de la directiva por la lista del conjunto global de usos de RTC. Preste atención a la sintaxis del valor del reemplazo: $a.Usage. Hace referencia a la propiedad Usage de la configuración de usos de RTC, que contiene la lista de usos de RTC.

    $a = Get-CsPstnUsage
    Set-CsVoicePolicy -Identity site:Redmond -PstnUsages @{replace=$a.Usage}

## Descripción detallada

Este cmdlet modifica una directiva de voz existente. Las directivas de voz se usan para administrar características de Telefonía IP empresarial, como las llamadas simultáneas (la posibilidad de recibir una segunda llamada cada vez que alguien llama al número de una oficina) o el desvío de llamadas. Use este cmdlet para cambiar la configuración que habilita y deshabilita muchas de estas características.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **Set-CsVoicePolicy** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicePolicy"}

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
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Si este parámetro está definido como True, los usuarios asignados a esta directiva pueden transferir llamadas. Si está definido en False, las llamadas no pueden transferirse.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Si este parámetro está definido como True, las llamadas a números internos de otro grupo de servidores se enrutarán a través de la red telefónica conmutada pública (RTC) si el grupo de servidores o la red WAN no está disponible.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Las llamadas simultáneas son una característica que permite que varios teléfonos reciban una misma llamada al marcar un solo número. Al definir este parámetro en True, se habilitan las llamadas simultáneas. Si el parámetro está definido en False, las llamadas simultáneas no pueden configurarse para ningún usuario que esté asignado a esta directiva.</p></td>
</tr>
<tr class="even">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Opcional</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Permite a los administradores administrar el reenvío de llamadas y las llamadas simultáneas. Los valores permitidos son:</p>
<p>* VoicePolicyUsage: el uso de directivas de voz predeterminado se utiliza para administrar el reenvío de llamadas y las llamadas simultáneas en todas las llamadas. Este es el valor predeterminado.</p>
<p>* InternalOnly: reenvío de llamadas y llamadas simultáneas se limitan a las llamadas realizadas desde un usuario de Lync a otro.</p>
<p>* CustomUsage: se utilizará un uso personalizado de RTC para administrar el reenvío de llamadas y las llamadas simultáneas. Este uso se debe especificar mediante el parámetro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>El uso personalizado de RTC que se usa para administrar el reenvío de llamadas y las llamadas simultáneas. Para agregar un uso personalizado a una directiva de voz, utilice una sintaxis similar a la siguiente:</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Para quitar un uso personalizado, utilice esta sintaxis:</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Tenga en cuenta que el uso debe existir ya para que se pueda utilizar con el parámetro CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Descripción de la directiva de voz.</p>
<p>Longitud máxima: 1040 caracteres.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Las directivas se pueden definir para limitar el ancho de banda y definir otras propiedades que estén relacionadas con la configuración de red. Al definir este parámetro en True, se permite la invalidación de las directivas. Es decir, si este parámetro está definido como True, no se realizarán comprobaciones de ancho de banda, y las llamadas se realizarán al margen de la configuración de control de admisión de llamadas (CAC).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>La Aplicación de estacionamiento de llamadas permite retener o estacionar una llamada en un determinado número dentro de un intervalo de números para recuperarla más tarde. Si se define este parámetro en True, se habilita esta aplicación para los usuarios asignados a esta directiva. Si está definido en False, los usuarios que estén asignados a esta directiva no podrán estacionar llamadas que se hayan marcado para su número de teléfono.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Determina si las llamadas se pueden transferir a otro número. Si este parámetro está definido en True, las llamadas pueden transferirse; si está definido en False, las llamadas no pueden transferirse.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>La delegación de llamada permite a un usuario responder a llamadas de otro usuario o hacer llamadas en nombre de otro usuario. Por ejemplo, un coordinador puede configurar la delegación de llamadas para que tanto su teléfono como el de un administrador reciban todas las llamadas entrantes. Al definir este parámetro en True, los usuarios con esta directiva pueden definir la delegación de llamadas. Al definir este parámetro en False, se deshabilita la delegación de llamadas.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>La grabación de llamadas malintencionadas es una opción estándar que se proporciona para grabar las llamadas que un usuario designe como malintencionadas. Las llamadas se pueden grabar aunque el ID del autor de la llamada esté bloqueado. La grabación solo está disponible para las autoridades apropiadas y, en ningún caso, para el usuario. Al definir esta propiedad en True, se habilita la posibilidad de establecer una grabación en las llamadas malintencionadas.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>La llamada de equipo permite a un usuario designar un grupo de usuarios cuyos teléfonos sonarán cuando el número del usuario reciba una llamada. Esta característica es útil en los equipos donde, por ejemplo, cualquiera de los miembros del equipo puede responder a las llamadas entrantes de clientes. Al definir este parámetro en True, se habilita esta característica.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Cuando se configura como True, las llamadas a un dispositivo móvil que no se respondan se reenviarán al correo de voz de la organización en lugar de al correo de voz del proveedor del dispositivo móvil. Si se responde a una llamada &quot;demasiado pronto&quot; (es decir, antes de que haya transcurrido el valor configurado para la propiedad PSTNVoicemailEscapeTimer), se asumirá que el dispositivo móvil no está disponible y la llamada se reenviará al correo de voz de la organización.</p>
<p>El valor predeterminado es False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime los mensajes de confirmación que, de lo contrario, se mostrarían antes de realizar cambios.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificador único que identifica el ámbito y, en algunos casos, el nombre de la directiva.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Opcional</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Permite transmitir una referencia a un objeto en el cmdlet en lugar de establecer valores de parámetro independientes. Este objeto debe ser de tipo VoicePolicy y puede recuperarse llamando al cmdlet <strong>Get-CsVoicePolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Opcional</p></td>
<td><p>Cadena</p></td>
<td><p>Un nombre descriptivo que identifica a esta directiva.</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Las tarifas de RTC se conocen más habitualmente como tarifas de larga distancia. En algunas ocasiones, las organizaciones pueden omitir estas tarifas mediante la implementación de una solución de voz sobre IP (VoIP), que permite a las sucursales conectarse mediante llamadas en red. Al definir este parámetro como True, las llamadas se enviarán a través de la RTC y esto conllevará gastos, en lugar de establecer la conexión a través de la red y evitar los pagos.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Opcional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Una lista de usos de RTC disponibles para esta directiva. El uso de RTC vincula una directiva de voz con una ruta telefónica.</p>
<p>Puede agregarse cualquier valor de cadena de caracteres a esta lista, siempre y cuando el valor exista en la lista de usos RTC global. (No están permitidas las cadenas de caracteres duplicadas. Todas las cadenas de caracteres deben ser únicas.) La lista de usos de RTC puede recuperarse llamando al cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Tenga en cuenta que si usa este parámetro para quitar todos los usos de RTC de la directiva, los usuarios con esta directiva no podrán realizar llamadas salientes a través de la red RTC.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Opcional</p></td>
<td><p>Int64</p></td>
<td><p>Cantidad de tiempo (en milisegundos) que se emplea para definir si se ha respondido a una llamada &quot;demasiado pronto&quot;. Si se recibe una respuesta dentro de este intervalo de tiempo, Lync Server supondrá que el dispositivo móvil no está disponible y desviará automáticamente la llamada al correo de voz de la organización. Si, al transcurrir el intervalo de tiempo, no se ha recibido respuesta, se permitirá que continúe la llamada.</p>
<p>El valor predeterminado es 1500 milisegundos.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Opcional</p></td>
<td><p>GUID</p></td>
<td><p>Identificador único global (GUID) de la cuenta del inquilino de Skype Empresarial Online cuya directiva de voz se va a modificar. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el Id. de inquilino de cada uno de los inquilinos, ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Objeto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Acepta la entrada por canalización de objetos de directiva de voz.

## Tipos de valores devueltos

Este cmdlet no devuelve un objeto o valor. En su lugar, configura instancias del objeto Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy.

## Vea también

#### Otros recursos

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

