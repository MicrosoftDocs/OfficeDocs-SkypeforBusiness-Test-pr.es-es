---
title: Get-CsTenant
TOCTitle: Get-CsTenant
ms:assetid: 7b642117-5ca7-4a5b-bca7-16b0ae694ae2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ994044(v=OCS.15)
ms:contentKeyID: 52061661
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenant

 

_**Última modificación del tema:** 2015-03-09_

Devuelve información sobre los inquilinos de Skype Empresarial Online que se han configurado para su uso en la organización. Los inquilinos representan grupos de usuarios en línea. En muchos casos, es posible que solo necesite un inquilino. Sin embargo, si hay varios grupos de usuarios con distintas necesidades de administración, Skype Empresarial Online ofrece respaldo a una sola organización que tenga varios inquilinos.

Get-CsTenant solo se puede usar con Skype Empresarial Online.

## Sintaxis

    Get-CsTenant [[-Identity] <OUIdParameter>] [-Filter <String>] [-ResultSize <Unlimited`1>] [-Verbose]

## Ejemplos

## Ejemplo 1

El comando del ejemplo 1 devuelve información sobre todos los inquilinos configurados para su uso en la organización.

    Get-CsTenant

## Ejemplo 2

En el ejemplo 2, se devuelve información sobre un solo inquilino: el inquilino con la identidad "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenant -Identity "bf19b7db-6960-41e5-a139-2aa373474354"

## Ejemplo 3

El comando anterior muestra una forma alternativa para devolver información sobre un solo inquilino; en este ejemplo, se hace incluyendo el parámetro Filter y el valor de filtro {DisplayName –eq "Fabrikam"}. Esta sintaxis devuelve información solo sobre el inquilino que tiene el nombre para mostrar Fabrikam.

    Get-CsTenant -Filter {DisplayName -eq "Fabrikam"}

## Ejemplo 4

El comando del ejemplo 4 devuelve información sobre todos los inquilinos que tienen una ServiceInstance igual a "LitwareincCommunicationsOnline/San Antonio". Para hacer esto, el comando incluye el parámetro Filter y el valor de filtro {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}. Este valor de filtro limita los datos devueltos a los inquilinos que tienen una propiedad ServiceInstance igual a (-eq) "LitwareincCommunicationsOnline/San Antonio".

    Get-CsTenant -Filter {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}

## Ejemplo 5

El ejemplo 5 devuelve información sobre todos los inquilinos que tienen un nombre para mostrar de país o región igual a Australia. Esto se hace usando el parámetro Filter y el valor de parámetro {CountryOrRegionDisplayName -eq "Australia"}.

    Get-CsTenant -Filter {CountryOrRegionDisplayName -eq "Australia"}

## Descripción detallada

En Skype Empresarial Online, los inquilinos representan grupos de usuarios que tienen cuentas hospedadas en el servicio. Muchas organizaciones necesitarán un solo inquilino en el que hospedar todas sus cuentas de usuario. Sin embargo, la administración de Skype Empresarial Online se suele hacer en cada inquilino por separado; esto significa que todos los usuarios del mismo inquilino tendrán la misma directiva de voz, las mismas opciones de configuración de federación, etc. Si necesita administrar algunos usuarios de cierto modo y otros usuarios de otra forma, puede usar varios inquilinos, cada uno con su propia colección de directivas y opciones de configuración.

Al margen del número de inquilinos que tenga, puede devolver información sobre estos inquilinos usando el cmdlet **Get-CsTenant**.

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
<td><p><em>Filter</em></p></td>
<td><p>Opcional</p></td>
<td><p>System.String</p></td>
<td><p>Le permite devolver datos usando atributos de Active Directory sin tener que especificar el nombre distintivo completo de Active Directory. Por ejemplo, para recuperar un inquilino usando el nombre para mostrar del inquilino, use una sintaxis como esta:</p>
<p>Get-CsTenant –Filter {DisplayName –eq &quot;FabrikamTenant&quot;}</p>
<p>Para devolver todos los inquilinos que usen un dominio de Fabrikam, use esta sintaxis:</p>
<p>Get-CsTenant –Filter {Domains –like &quot;*fabrikam*&quot;}</p>
<p>El parámetro Filter usa la misma sintaxis de filtrado de Windows PowerShell que usa el cmdlet Where-Object.</p>
<p>No puede usar los parámetros Identity y Filter en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Nombre distintivo de Active Directory del inquilino. Por ejemplo:</p>
<p>-Identity &quot;OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=litwareinc,dc=com&quot;</p>
<p>Si no incluye el parámetro Identity o Filter, el cmdlet <strong>Get-CsTenant</strong> devuelve información sobre todos los inquilinos.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Opcional</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited`1</p></td>
<td><p>Permite limitar el número de registros que devuelve el cmdlet. Por ejemplo, para que se devuelvan siete inquilinos (al margen de la cantidad de inquilinos que haya en el bosque), incluya el parámetro ResultSize y defina el valor de parámetro en 7. Recuerde que no es posible especificar qué 7 usuarios se devolverán.</p>
<p>El tamaño de los resultados puede definirse en cualquier número entero entre 0 y 2147483647, ambos incluidos. Si se establece en 0, el comando se ejecutará pero no devolverá datos. Si se definen los inquilinos en 7 pero solo hay tres contactos en el bosque, el comando devolverá esos tres inquilinos y se completará sin errores.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

El cmdlet **Get-CsTenant** acepta instancias canalizadas del objeto Microsoft.Rtc.Management.ADConnect.Schema.TenantObject y valores de cadena que representan la identidad de un inquilino de Skype Empresarial Online (por ejemplo, "OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=vdomain,dc=com").

## Tipos de valores devueltos

El cmdlet **Get-CsTenant** devuelve instancias del objeto Microsoft.Rtc.Management.ADConnect.Schema.TenantObject.

## Vea también

#### Otros recursos

[Get-CsOnlineUser](get-csonlineuser.md)

