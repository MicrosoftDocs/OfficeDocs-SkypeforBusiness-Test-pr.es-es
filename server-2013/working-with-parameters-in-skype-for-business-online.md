---
title: Trabajar con parámetros
TOCTitle: Trabajar con parámetros
ms:assetid: 29ebda0f-ae5f-4512-ad59-240c3605b240
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362778(v=OCS.15)
ms:contentKeyID: 56271272
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Trabajar con parámetros

 

_**Última modificación del tema:** 2015-06-22_

Al usar el parámetro Identity, verá que el valor de parámetro kenmyer@litwareinc.com está encerrado entre comillas dobles:

    -Identity "kenmyer@litwareinc.com"

Una de las preguntas que todas las personas que empiezan a usar Windows PowerShell hacen es esta: ¿cuándo tengo que usar comillas dobles y cuándo no? No existe una respuesta simple a esta pregunta, pero existen unas reglas generales que se deben seguir:

  - Normalmente, las comillas dobles no son necesarias cuando el valor de parámetro es un número. Por ejemplo, para limitar el número de usuarios que devuelve el cmdlet [Get-CsOnlineUser](get-csonlineuser.md), se usa esta sintaxis:
    
        -ResultSize 100
    
    De hecho, nunca se deben usar las comillas dobles para encerrar un número. Si se hace, es posible que Windows PowerShell no pueda interpretar el valor como número.
    
    De igual modo, debe asegurarse de no incluir comas en los números. Por ejemplo, si quisiera establecer el tamaño de resultados en 10.000, la sintaxis siguiente sería incorrecta:
    
        -ResultSize 10,000
    
    Esta sintaxis provoca un error porque Windows PowerShell usa la coma para separar valores de argumento. En este caso Windows PowerShell, interpretará que quiere pasar dos valores de parámetro distintos: 10 y 000. Como el tamaño de resultados no se puede establecer a la vez en 10 y en 0, se produce un error. Debe usar esta sintaxis sin coma:
    
        -ResultSize 10000

  - Las comillas dobles tampoco suelen ser necesarias cuando el valor de parámetro es una fecha:
    
        -StartDate 6/1/2013
    
    Pero esto solo se cumple cuando no se incluye la hora. Al incluir la hora (que implica poner un espacio en blanco entre la fecha y la hora), el valor de parámetro se debe encerrar entre comillas dobles:
    
        -StartDate "6/1/2013 10:00AM"
    
    Tenga en cuenta que el comando anterior tiene el formato de los equipos que usan Inglés (EE. UU.) como configuración regional. Si no usa Inglés (EE. UU.), debe escribir las fechas y horas con el formato correspondiente a la configuración de su equipo. Para ver qué configuración regional usa Windows PowerShell, ejecute este comando desde el símbolo del sistema de Windows PowerShell:
    
        Get-Host | Select-Object CurrentUICulture

  - Los valores de cadena (como los nombres de persona) no suelen necesitar comillas dobles. Las principales excepciones se dan en los valores de cadena que incluyen caracteres restringidos, como un espacio en blanco, una coma u otros signos de puntuación. Por ejemplo, esta sintaxis funciona porque la identidad del usuario no incluye ningún carácter restringido:
    
        -Identity "kenmyer@litwareinc.com"
    
    Sin embargo, este comando dará error porque la identidad incluye un espacio en blanco:
    
        -Identity Ken Myer
    
    El comando anterior no funciona porque Windows PowerShell usa espacios en blanco para separar un parámetro de otro. Esto significa que Windows PowerShell interpreta que el parámetro Identity es Ken y que Myer es otro parámetro distinto. Como resultado, aparece el siguiente mensaje de error:
    
        Get-CsOnlineUser : No se puede encontrar ningún parámetro de posición que acepte el argumento "Myer".
    
    Para usar un valor de parámetro que incluya un espacio en blanco (o una coma u otro carácter restringido), encierre el valor entre comillas dobles:
    
        -Identity "Ken Myer"
    
    En la mayoría de los casos, Windows PowerShell permite usar comillas simples en lugar de comillas dobles. Por ejemplo, esta sintaxis de Windows PowerShell es válida:
    
        -Identity 'Ken Myer'
    
    Sin embargo, recuerde que debe usar el mismo tipo de comillas al principio y al final de la cadena. Es decir, la siguiente sintaxis de Windows PowerShell no es válida:
    
        -Identity "Ken Myer'
    
    Si intenta ejecutar este comando, verá lo siguiente en la consola de Windows PowerShell:
    
    ``` 
    >>
    ```
    
    La flecha doble es la forma de pedirle que complete el comando: como empieza con comillas dobles, Windows PowerShell espera que termine también con comillas dobles. Si sale el aviso \>\>, presione Ctrl-C para cancelar el comando y vuelva a intentarlo.

  - Las comillas dobles no se deben usar con valores booleanos (True/False). Además, es necesario usar las variables $True y $False de Windows PowerShell al especificar los valores True y False. Por ejemplo:
    
        -EnterpriseVoiceEnabled $True

También hay ciertos parámetros de Windows PowerShell denominados *parámetros de modificador* que no aceptan valores de parámetro:

    -WhatIf

Los valores de parámetro no solo no son necesarios al usar un parámetro de modificador, sino que, al incluirlos, se genera un error. Por ejemplo, si intenta ejecutar este comando:

    -WhatIf $True

Este comando producirá un mensaje de error parecido a este:

    Set-CsUserAcp :  No se puede encontrar ningún parámetro de posición que acepte el argumento "True"

Para administrar Skype Empresarial Online con Windows PowerShell, debe saber qué cmdlets pueden usarse. También debe conocer los parámetros disponibles para cada cmdlet, así como el *tipo de datos* de cada parámetro (es decir, si el parámetro acepta un valor de datos, un valor de cadena, etc.). Esta información (y muchos ejemplos de uso de los cmdlets) la encontrará en los temas de Ayuda de los cmdlets de Skype Empresarial Online. Por ejemplo, estos son los parámetros que se pueden usar con el cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md):

![Parámetros de un cmdlet de PowerShell específico](images/Dn362778.ead7add1-eec3-4fa4-8bbe-9aa72bb7a1ae(OCS.15).png "Parámetros de un cmdlet de PowerShell específico")

Como puede ver, la tabla de parámetros ofrece la descripción de cada cmdlet e indica el tipo de datos de cada parámetro y si el parámetro es necesario (obligatorio) u opcional. El tipo de datos mostrado en la tabla es el tipo de datos oficial que usa .NET Framework. Esto significa que el tipo de datos se muestra como System.Management.Automation.SwitchParameter en lugar de solo como "Switch Parameter" (parámetro de modificador). A continuación, presentamos una guía rápida sobre los tipos de datos que los cmdlets de Skype Empresarial Online usan con más frecuencia:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Un valor de cadena que representa la identidad de un usuario. Suele ser el UPN o la dirección SIP del usuario:</p>
<pre><code>-Identity &quot;kenmyer@litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Un FQDN es un nombre de dominio completo. Por ejemplo:</p>
<pre><code>-Fqdn &quot;atl-lync-001.litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Boolean</p></td>
<td><p>Un valor booleano es un valor True/False. Recuerde que debe usar las variables de Windows PowerShell $True y $False al especificar valores booleanos:</p>
<pre><code>-Enabled $True -EnterpriseVoiceEnabled $False</code></pre></td>
</tr>
<tr class="even">
<td><p>Identificador único global</p></td>
<td><p>GUID es el acrónimo de <em>identificador único global</em>, un identificador único que, en Skype Empresarial Online, se asigna a cada inquilino de Skype Empresarial Online. Por ejemplo:</p>
<pre><code>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</code></pre>
<p>Puede recuperar el GUID asignado a sus inquilinos de Skype Empresarial Online usando este comando:</p>
<pre><code>Get-CsTenant | Select-Object TenantId</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Los parámetros de modificador reciben este nombre porque están activados o desactivados. Si el parámetro está presente, entonces el modificador está, por así decirlo, activado; si el parámetro no está presente, el modificador está desactivado. Por ejemplo, si quiere usar el parámetro Confirm para pedir confirmación antes de ejecutar un comando, hay que incluir el parámetro Confirm (sin valor de parámetro) como parte del comando. Por ejemplo:</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot; -Confirm</code></pre>
<p>Si no quiere pedir confirmación, no incluya el parámetro Confirm:</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>System.String</p></td>
<td><p>Un valor de cadena es un valor alfanumérico, es decir, que puede contener (en general) cualquier carácter que se pueda escribir con el teclado. Por ejemplo:</p>
<pre><code>-Password &quot;abc123%&amp;*&quot;</code></pre>
<p>Es aconsejable encerrar los valores de cadena entre comillas dobles. No siempre es obligatorio, pero sí es necesario cuando el valor de cadena contiene un espacio en blanco o una coma, o si se trata de una palabra clave de Windows PowerShell reservada. (Una palabra clave es un comando u otro elemento que forma parte del propio lenguaje de Windows PowerShell. Por ejemplo, “If” y “End” son palabras clave de Windows PowerShell). Para más información, escriba el comando siguiente desde el símbolo del sistema de Windows PowerShell:</p>
<p>Get-Help about_Reserved_Words</p></td>
</tr>
</tbody>
</table>


## Vea también

#### Conceptos

[Introducción a Windows PowerShell y Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

