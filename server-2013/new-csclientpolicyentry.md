---
title: New-CsClientPolicyEntry
TOCTitle: New-CsClientPolicyEntry
ms:assetid: e975d048-4911-4ae6-9446-2a6363726a4a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg399046(v=OCS.15)
ms:contentKeyID: 48277049
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicyEntry

 

_**Última modificación del tema:** 2015-03-09_

Agrega opciones nuevas a las directivas de cliente de Lync Server. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsClientPolicyEntry -Name <String> -Value <String>

## Ejemplos

## Ejemplo 1

Los comandos del ejemplo 1 muestran cómo agregar una nueva entrada de directiva a la directiva de cliente global. Este ejemplo agrega una nueva opción de comentarios a Lync. Debe tener en cuenta que este es un ejemplo demostrativo. No es posible ejecutar estos comandos para agregar una opción de comentarios similar en su copia de Lync.

Para agregar la entrada de directiva, el primer comando del ejemplo usa el cmdlet **New-CsClientPolicyEntry** para crear una entrada con el nombre OnlineFeedbackURL y el valor http://www.litwareinc.com/feedback. El objeto de entrada de directiva resultante se almacena en una variable llamada $x.

En el segundo comando, se usa el cmdlet **Get-CsClientPolicy** para crear una referencia de objeto ($y) a la directiva de cliente global. Una vez creada la referencia de objeto, se usa el método Add para agregar la nueva entrada de directiva a la propiedad PolicyEntry. Si PolicyEntry ya tiene una o varias entradas, el nuevo valor se anexará al final de la recopilación.

Finalmente, el último comando del ejemplo usa el cmdlet **Set-CsClientPolicy** para escribir los cambios en la directiva global real. Si no se llama al cmdlet **Set-CsClientPolicy**, los cambios solo se aplicarán en la memoria, y desaparecerán al finalizar la sesión de Windows PowerShell o eliminar la variable $x.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    
    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.Add($x)
    
    Set-CsClientPolicy -Instance $y

## Ejemplo 2

El ejemplo 2 es una variación de los comandos que aparecen en el ejemplo 1. En este caso, la nueva entrada de directiva reemplaza todos los elementos que se encuentran en la propiedad PolicyEntry de la directiva global. Para ello, el primer comando del ejemplo crea una entrada de directiva que se almacena en una variable llamada $x. A continuación, el segundo comando usa el cmdlet **Set-CsClientPolicy** para configurar el valor de la propiedad PolicyEntry como $x. Una vez finalice la ejecución del comando, el único elemento de la propiedad PolicyEntry será la nueva entrada. Todos los elementos que contenía esa propiedad antes de llamar al cmdlet **Set-CsClientPolicy** se habrán reemplazado por la entrada nueva.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    Set-CsClientPolicy -Identity global -PolicyEntry $x

## Ejemplo 3

El Ejemplo 3 muestra cómo quitar una entrada de directiva de cliente de la directiva global. Para hacerlo, el primer comando del ejemplo recupera la directiva de cliente global y almacena la información en una variable llamada $y.

Después de recuperar la directiva global, el segundo comando del ejemplo utiliza el método RemoveAt() para eliminar la primera entrada de directiva de esa directiva. La entrada de directiva que se quitará se indica con el número de índice: la primera entrada de la directiva tiene un número de índice de 0; la segunda, 1, etc. La sintaxis RemoveAt(0) significa que se quitará la primera entrada de la directiva.

En cuanto se quita la entrada de directiva de la instancia de la directiva global que hay en la memoria, se llama al cmdlet **Set-CsClientPolicy** para escribir los cambios en la instancia real de la directiva de cliente global.

    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.RemoveAt(0)
    
    Set-CsClientPolicy -Instance $y 

## Ejemplo 4

El comando que aparece en el ejemplo 4 quita todas las entradas de directiva de cliente configuradas para la directiva global. Para ello, se utiliza el parámetro PolicyEntry y se establece el valor de parámetro como nulo ($Null).

    Set-CsClientPolicy -Identity global -PolicyEntry $Null

## Descripción detallada

Las directivas de cliente son el mecanismo principal que utiliza Lync Server para administrar el software cliente como Lync. Al crear o configurar una directiva de cliente, tiene diversas opciones disponibles; por ejemplo, puede especificar si desea que se puedan utilizar fotos en Lync, si se permite incluir emoticonos en los mensajes instantáneos, y si Lync guarda automáticamente transcripciones de las sesiones de mensajería instantánea. Estas opciones abarcan muchas de las configuraciones relacionadas con el cliente que necesitan controlar los administradores.

Sin embargo, es posible que no abarquen todas las opciones de configuración de los clientes que necesiten controlar los administradores. Para administrar las opciones de manera más flexible y exhaustiva, las directivas de cliente incluyen una propiedad llamada PolicyEntry. Esta propiedad multivalor permite a los administradores agregar nuevas opciones de administración que no están incluidas expresamente en las directivas de cliente. Por ejemplo, antes del lanzamiento de Lync Server, los participantes en las pruebas beta podían agregar una opción de comentarios a Lync. Esta opción se agregó como una nueva entrada de directiva y se creó utilizando el cmdlet **New-CsClientPolicyEntry**.

Debe tener en cuenta que no es posible crear entradas de directiva de manera arbitraria y pretender administrar Lync u otras aplicaciones cliente con ellas. Es necesario esperar a obtener información de Microsoft sobre los nombres y valores que pueden usarse para crear entradas de directivas de cliente.

Quién puede ejecutar este cmdlet: de forma predeterminada, están autorizados para ejecutar el cmdlet **New-CsClientPolicyEntry** localmente los miembros de los siguientes grupos: RTCUniversalServerAdmins. Para devolver una lista de todos los roles de control de acceso basado en roles (RBAC) a los que se asignó este cmdlet (incluidos los roles de RBAC personalizados que haya creado), ejecute el siguiente comando en el símbolo del sistema de Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicyEntry"}

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
<td><p><em>Name</em></p></td>
<td><p>Requerido</p></td>
<td><p>System.String</p></td>
<td><p>Nombre de la nueva entrada de directiva. Por ejemplo: -Name &quot;OnlineFeedbackURL&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Value</em></p></td>
<td><p>Requerido</p></td>
<td><p>System.String</p></td>
<td><p>Valor que se asignará a la nueva entrada de directiva. Por ejemplo: -Value http://www.litwareinc.com/feedback.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet New-CsClientPolicyEntry no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **New-CsClientPolicyEntry** crea nuevas instancias del objeto Microsoft.Rtc.Management.WritableConfig.Policy.Client.PolicyEntryType.

## Vea también

#### Otros recursos

[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

