---
title: New-CsDialInConferencingConfiguration
TOCTitle: New-CsDialInConferencingConfiguration
ms:assetid: ac0b6e22-3883-4884-aa94-18f4029c7f1e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412816(v=OCS.15)
ms:contentKeyID: 48276336
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingConfiguration

 

_**Última modificación del tema:** 2015-03-09_

Crea una colección de opciones de configuración de conferencias de acceso telefónico local. Estos valores determinan cómo responde Lync Server cuando los usuarios entran o salen de una conferencia de acceso telefónico local. Concretamente, la información se devuelve dependiendo de si es necesario o no que los participantes graben su nombre cuando se unen a una conferencia y de cómo (o si) el sistema anuncia que alguien se ha unido a la conferencia o la ha abandonado. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 crea una nueva colección de valores de configuración de conferencias de acceso telefónico que se aplican al sitio Redmond. Además, el parámetro opcional EnableNameRecording se incluye para establecer la propiedad EnableNameRecording como False.

    New-CSDialInConferencingConfiguration -Identity site:Redmond -EnableNameRecording $False

## Ejemplo 2

En el ejemplo 2, el parámetro InMemory se usa para crear una nueva colección de valores de configuración de conferencia de acceso telefónico local que, en principio, existen solo en la memoria. Para ello, en el ejemplo se llama primero al cmdlet **New-CSDialInConferencingConfiguration** y al parámetro InMemory para crear una colección de configuraciones virtuales que se almacenan en la variable $x (tenga en cuenta que esta colección recibe la identidad site:Redmond). Después de crear la colección virtual, la línea 2 se usa para modificar el valor de la propiedad EnableNameRecording. Para terminar, la línea 3 del ejemplo llama al cmdlet **Set-CSDialInConferencingConfiguration** para transformar los valores de configuración virtual almacenados en $x en una colección real de valores aplicada al sitio Redmond.

    $x = New-CSDialInConferencingConfiguration -Identity site:Redmond -InMemory
    $x.EnableNameRecording = $False
    Set-CSDialInConferencingConfiguration -Instance $x

## Descripción detallada

Cuando los usuarios se unen a una conferencia de acceso telefónico (o la abandonan), Lync Server puede responder de diferentes maneras. Por ejemplo, se les podría pedir a los participantes que registren su nombre antes de unirse a la conferencia. Del mismo modo, los administradores pueden decidir si desean que Lync Server anuncie que los participantes de acceso telefónico local dejaron o se unieron a la conferencia.

Estos "comportamientos de unión" de conferencias se administran con los valores de configuración de conferencias de acceso telefónico. Estos valores pueden configurarse en ámbito global o en ámbito de sitio. (Las opciones configuradas en el ámbito del sitio tienen precedencia sobre las opciones configuradas en el ámbito global). Cuando instala por primera vez Lync Server, los únicos valores de configuración de conferencias de acceso telefónico que tendrá serán los de ámbito global. Sin embargo, puede crear nuevos en el ámbito de sitio con el cmdlet **New-CSDialInConferencingConfiguration**.

Quién puede iniciar este cmdlet: de forma predeterminada, los miembros de los siguientes grupos están autorizados a iniciar el cmdlet **New-CsDialInConferencingConfiguration** localmente: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluyendo todos los roles RBAC personalizados que haya creado), inicie el siguiente comando desde el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingConfiguration"}

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
<td><p>Indica la identidad de los valores de configuración de las conferencias de acceso telefónico que se han de crear. Debido a que estos valores solo pueden crearse en el ámbito de sitio, use una sintaxis similar a la siguiente, con el prefijo &quot;site:&quot; seguidos por el nombre del sitio: -Identity site:Redmond.</p>
<p>Tenga en cuenta que únicamente puede haber un conjunto de valores de configuración de conferencias de acceso telefónico por sitio. El comando de ejemplo dará error si ya existe una colección de valores con la identidad site:Redmond.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNameRecording</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Determina si se pedirá a los usuarios que graben su nombre antes de entrar en la conferencia. Se configura como True ($True) para pedir la grabación de los nombres. Se configura como False ($False) para omitirla. El valor predeterminado es True.</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>Opcional</p></td>
<td><p>Booleano</p></td>
<td><p>Si está configurado como True, se reproducirá un anuncio cada vez que un participante entre o salga de una conferencia. Si está configurado como False (el valor predeterminado), no se reproducirá ningún anuncio de entrada y salida.</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>Opcional</p></td>
<td><p>EntryExitAnnouncementsType</p></td>
<td><p>Indica la acción que realiza el sistema cada vez que un participante entra en una conferencia o la abandona. Los valores válidos son:</p>
<p>UseNames: el nombre de la persona se anuncia cada vez que entra a una conferencia o la abandona (por ejemplo, &quot;Ken Myer ha salido de la conferencia&quot;).</p>
<p>ToneOnly: se reproduce un tono cada vez que un participante entra en una conferencia o la abandona.</p>
<p>El valor predeterminado es UseNames. Observe que los anuncios se muestran únicamente si la propiedad EntryExitAnnouncementsEnabledByDefault está definida en True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suprime la visualización de los mensajes de error que no sean graves que se puedan producir al iniciar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Opcional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
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

Ninguno. El cmdlet **New-CsDialInConferencingConfiguration** no acepta entradas canalizadas.

## Tipos de valores devueltos

Crea nuevas instancias del objeto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration.

## Vea también

#### Otros recursos

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

