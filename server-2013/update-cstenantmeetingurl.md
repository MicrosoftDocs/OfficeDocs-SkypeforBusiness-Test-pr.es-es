---
title: Update-CsTenantMeetingUrl
TOCTitle: Update-CsTenantMeetingUrl
ms:assetid: 9aed3ede-bbd3-405a-997f-f7553e66aecd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn424754(v=OCS.15)
ms:contentKeyID: 59602842
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsTenantMeetingUrl

 

_**Última modificación del tema:** 2015-03-09_

Actualiza la URL de reunión del inquilino de Skype Empresarial Online especificado. La URL actualizada usa un formato más simple y estandarizado que permite a los clientes buscar reuniones y conectarse a ellas con mayor facilidad.

Este cmdlet está pensado para usarse solo con Skype Empresarial Online.

## Sintaxis

    Update-CsTenantMeetingUrl [-Tenant] <guid> [-Force] [-WhatIf] [-Confirm]

## Ejemplos

## Ejemplos 1

El comando que se muestra en el ejemplo 1 actualiza la URL de reunión del inquilino con identificador 38aad667-af54-4397-aaa7-e94c79ec2308. (Tenga en cuenta que debe proporcionar el identificador de inquilino para que se complete este comando). Después de presionar ENTRAR para ejecutar el comando, se le preguntará si está seguro de que quiere actualizar la URL de reunión. Debe responder que sí para que Update-CsTenantMeetingUrl pueda realizar cambios en la configuración de Skype Empresarial Online.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308"

## Ejemplos 2

El ejemplo 2 también actualiza la URL de reunión del inquilino con identificador 38aad667-af54-4397-aaa7-e94c79ec2308. Pero, en este caso, se incluye el parámetro Force, que omite el mensaje de confirmación que suele aparecer al ejecutar Update-CsTenantMeetingUrl. Entonces, apenas presione ENTRAR, se ejecutará el comando y se modificará la configuración de Skype Empresarial Online.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -Force

## Descripción detallada

Update-CsTenantMeetingUrl actualiza la URL de reunión de Skype Empresarial Online en un formato más simple y estandarizado, lo que ayuda a eliminar los problemas que solían ocasionarse con la URL de reunión original. Por ejemplo, suponga que una organización configura un dominio de Office 365 con el nombre contoso.onmicrosoft.com. Al hacerlo, las reuniones tendrán URL similares a esta:

https://meet.lync.com/onmicrosoft/contoso/user1/45GZFH99

Ahora bien, suponga que en la organización se realizan algunos cambios y se decide usar la URL mnemónica litwareinc.com en lugar de onmicrosoft.com. La organización modifica las direcciones de correo electrónico de los usuarios para usar el dominio litwareinc.com. Pero las URL de reunión seguirán usando el nombre de dominio antiguo:

https://meet.lync.com/contoso/user1/45GZFH99

Para solucionar este problema, los administradores deben ejecutar el cmdlet Update-CsTenantMeetingUrl, que reemplazará la URL de reunión antigua por la nueva URL mnemónica:

https://meet.lync.com/litwareinc.com/user1/37JYLP71

La única forma de hacer este cambio es ejecutando el cmdlet Update-CsTenantMeetingUrl.

Tenga en cuenta que, al ejecutar Update-CsTenantMeetingUrl, el inquilino de Skype Empresarial Online cambiará a la URL nueva tras un breve retraso de sincronización. Esto no creará ningún problema con las reuniones nuevas que los usuarios programen, ya que se programarán automáticamente con la URL nueva. Sin embargo, sí se ocasionarán problemas en las reuniones programadas con anterioridad, ya que se programaron con la URL de reunión antigua, que está inactiva. La única forma en que los usuarios pueden solucionar este problema es reprogramando las reuniones.

Como esto puede traer problemas en algunas organizaciones (en particular, en organizaciones en que ya se ha programado un gran número de reuniones), Update-CsTenantMeetingUrl le preguntará de forma predeterminada antes de actualizar la URL de reunión:

ADVERTENCIA: este es un cambio drástico para los usuarios que usan este inquilino. Se actualizará la configuración de URL de reunión. Las URL de reunión antiguas ya no funcionarán. Este cambio no se puede revertir.  
¿Está seguro de que quiere continuar?  
\[S\] Sí \[A\] Sí a todo \[N\] No \[L\] No a todo \[S\] Suspender \[?\] Ayuda (el valor predeterminado es “Y”):

Debe responder “Sí” o “Sí a todo” para que el comando se ejecute. Si responde “No”, se cancelará el comando y no se actualizará la URL de reunión. Tenga en cuenta que, una vez cambiada la URL de reunión, no hay forma de revertirla a la original. Una vez que se ejecute el comando, la URL se modificará y todas las reuniones programadas con anterioridad deberán reprogramarse. Esto también significa que solo es necesario ejecutar este comando una vez por cada inquilino. No hace falta ejecutarlo de forma periódica ni volver a actualizar la URL de reunión.

Si prefiere ejecutar el comando sin tener que responder al mensaje de confirmación, puede incluir el parámetro Force. Si lo hace, Update-CsTenantMeetingUrl se ejecutará sin mostrar el mensaje:

ADVERTENCIA: este es un cambio drástico para los usuarios que usan este inquilino. Se actualizará la configuración de URL de reunión.

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
<td><p><strong>Inquilino</strong></p></td>
<td><p>Obligatorio</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificador único global (GUID) de la cuenta de inquilino cuya configuración de federación se está devolviendo. Por ejemplo:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Para devolver el identificador de inquilino para cada uno de los inquilinos, ejecute este comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si no incluye el parámetro Tenant, Update-CsMeetingUrl le pedirá que lo escriba para continuar.</p></td>
</tr>
<tr class="even">
<td><p><strong>Confirmar</strong></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Le pide confirmación antes de ejecutar el comando.</p>
<p>Tenga en cuenta que el comportamiento predeterminado de Update-CsMeetingUrl es mostrar el mensaje de confirmación antes de realizar actualizaciones. Esto significa que, si quiere mostrar el mensaje, no es necesario incluir el parámetro Confirm.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Force</strong></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Hace que no se muestre el mensaje de confirmación que aparece antes de realizar actualizaciones con Update-CsMeetingUrl.</p></td>
</tr>
<tr class="even">
<td><p><strong>WhatIf</strong></p></td>
<td><p>Opcional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipos de entrada

Ninguno. Update-CsMeetingUrl no acepta entradas canalizadas.

## Tipos de valores devueltos

Ninguno.

## Vea también

#### Otros recursos

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

