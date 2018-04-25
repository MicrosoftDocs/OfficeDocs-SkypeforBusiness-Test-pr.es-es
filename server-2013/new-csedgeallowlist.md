---
title: New-CsEdgeAllowList
TOCTitle: New-CsEdgeAllowList
ms:assetid: 21a6d546-9e03-485c-b7ec-9deb778f2b01
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994023(v=OCS.15)
ms:contentKeyID: 52061609
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowList

 

_**Última modificación del tema:** 2015-03-09_

Permite a los administradores especificar los dominios con los que sus usuarios podrán comunicarse. El cmdlet **New-CsEdgeAllowList**, que solo se puede usar con Microsoft Lync Online, debe usarse con los cmdlets **New-CsEdgeDomainPattern** y **Set-CsTenantFederationConfiguration**.

## Sintaxis

    New-CsEdgeAllowList [-AllowedDomain <PSListModifier>] [-Verbose]

## Ejemplos

## Ejemplo 1

Los comandos del ejemplo 1 asignan el dominio fabrikam.com a la lista de dominios permitidos para el inquilino cuyo TenantId es "bf19b7db-6960-41e5-a139-2aa373474354". Para ello, el primer comando del ejemplo usa el cmdlet **New-CsEdgeDomainPattern** para crear un objeto de dominio para fabrikam.com; este objeto se almacena en una variable denominada $x. Cuando se ha creado el objeto de dominio, se usa el cmdlet **New-CsEdgeAllowList** para crear una lista permitida nueva que solo contiene el dominio fabrikam.com.

Con la lista de dominios permitidos creada, el último comando del ejemplo puede usar el cmdlet **Set-CsTenantFederationConfiguration** para configurar fabrikam.com como el único dominio de la lista de dominios permitidos para el inquilino indicado.

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Recuerde que el parámetro Tenant solo es necesario en implementaciones híbridas. Si solo está conectado a Skype Empresarial Online, el parámetro Tenant se puede omitir.

## Ejemplo 2

En el ejemplo 2 se ve cómo agregar varios dominios a una lista de dominios permitidos. Esto se hace llamando al cmdlet **New-CsEdgeDomainPattern** varias veces (una por cada dominio que se vaya a agregar a la lista) y almacenando los objetos de dominio resultantes en variables diferentes. Cada una de estas variables se puede luego agregar a la lista de permitidos que ha creado el cmdlet **New-CsEdgeAllowList** usando el parámetro AllowedDomain y separando los nombres de las variables con comas:

$newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y

    $x = New-CsEdgeDomainPattern -Domain "contoso.com"
    $y = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Ejemplo 3

En el ejemplo 3, todos los dominios se quitan de la lista de dominios permitidos. Para ello, el primer comando del ejemplo usa el cmdlet **New-CsEdgeAllowList** para crear una lista vacía de dominios permitidos; esto se hace estableciendo la propiedad AllowedDomain en un valor nulo ($Null). La referencia de objeto resultante ($newAllowList) se usa luego con el cmdlet **Set-CsTenantFederationConfiguration** para quitar todos los dominios de la lista de dominios permitidos para el inquilino cuyo TenantId es "bf19b7db-6960-41e5-a139-2aa373474354".

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $Null
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Descripción detallada

La federación es un servicio que permite a los usuarios intercambiar mensajes instantáneos e información de presencia con usuarios de otros dominios. Con Lync Online, los administradores pueden usar las opciones de configuración de federación para controlar:

  - Si los usuarios pueden o no comunicarse con personas de otros dominios y, en caso afirmativo, con qué dominios se pueden comunicar.

  - Si los usuarios pueden o no comunicarse con personas que tengan cuentas en proveedores de presencia y mensajería instantánea pública, como Windows Live, AOL y Yahoo.

La federación se administra, en parte, usando listas de dominios permitidos y dominios bloqueados. La lista de dominios permitidos contiene los dominios con los que los usuarios pueden comunicarse, mientras que la lista de dominios bloqueados contiene los dominios con los que no pueden comunicarse. De manera predeterminada, los usuarios pueden comunicarse con cualquier dominio que no aparezca en la lista de bloqueados, pero los administradores pueden modificar esta configuración predeterminada y limitar la comunicación a los dominios que aparecen en la lista de dominios permitidos.

Lync Online no permite modificar directamente la lista de permitidos ni la de bloqueados; por ejemplo, no se puede usar un comando parecido a este, que pasa un valor de cadena que representa un nombre de dominio a la lista de dominios permitidos:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

Tendrá que usar el cmdlet **New-CsEdgeAllowAllKnownDomains** o el cmdlet **New-CsEdgeAllowList** para crear un objeto de dominio y luego pasarlo al cmdlet **Set-CsTenantFederationConfiguration**. El cmdlet **New-CsEdgeAllowAllKnownDomains** se usa cuando se quiere permitir a los usuarios comunicarse con todos los dominios excepto con los que están en la lista de dominios bloqueados. El cmdlet **New-CsEdgeAllowList** se usa cuando se quiere limitar la comunicación de los usuarios a una colección concreta de dominios. En este caso, los usuarios solo se podrán comunicar con los dominios que aparezcan en la lista de dominios permitidos.

Para agregar un solo dominio (fabrikam.com) a la lista de dominios permitidos, tiene que usar un conjunto de comandos parecidos a estos:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Cuando este comando termine de ejecutarse, los usuarios solo podrán comunicarse con usuarios del dominio fabrikam.com.

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
<td><p><em>AllowedDomain</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Referencia de objeto al dominio (o conjunto de dominios) nuevo que se quiere agregar a la lista de dominios permitidos. Las referencias de objetos de dominios se deben crear usando el cmdlet <strong>New-CsEdgeDomainPattern</strong>. Se pueden agregar varios objetos de dominio separando las referencias de objeto con comas. Por ejemplo:</p>
<p>-AllowedDomain $x,$y</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. El cmdlet **New-CsEdgeAllowList** no acepta entradas canalizadas.

## Tipos de valores devueltos

El cmdlet **New-CsEdgeAllowList** crea instancias nuevas del objeto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowList.

## Vea también

#### Otros recursos

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

