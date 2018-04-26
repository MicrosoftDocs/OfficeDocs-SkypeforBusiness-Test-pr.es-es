---
title: Cmdlets de servidor perimetral
TOCTitle: Cmdlets de servidor perimetral
ms:assetid: 1a5427f4-a0d1-4652-8135-91333158ffc8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg415635(v=OCS.15)
ms:contentKeyID: 48274582
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets de servidor perimetral

 

_**Última modificación del tema:** 2016-12-08_

Los servidores perimetrales permiten ampliar las prestaciones de Microsoft Lync Server 2013 para las personas que no hayan iniciado sesión en la red interna. Por ejemplo, si tiene usuarios remotos, es decir, usuarios autenticados que inician sesión en Lync Server 2013 por Internet en lugar de la red interna, necesitará configurar un servidor perimetral que ejecute el servicio perimetral de acceso de Lync Server. Además, los servidores perimetrales son necesarios si desea establecer una federación con otra organización o si desea brindar a sus usuarios el derecho a comunicarse con personas que tienen cuentas con un servicio de mensajería instantánea pública como Yahoo\!, AOL o MSN.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg425917.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>El 1 de septiembre de 2012, la licencia de suscripción del usuario de Public IM Connectivity de Microsoft Lync (&quot;PIC USL&quot;) dejó de estar disponible para su compra en los contratos nuevos y en las prórrogas de contratos. Los clientes que tengan licencias activas podrán seguir federándose con Yahoo! Messenger hasta la fecha de cierre del servicio. La fecha anunciada para el fin de vida de AOL y Yahoo! es junio de 2014. Para más detalles, vea <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Soporte para la conectividad de mensajería instantánea pública en Lync Server 2013</a>.</p></li>
<li><p>PIC USL es una licencia de suscripción por usuario/por mes requerida por Lync Server u Office Communications Server para la federación con Yahoo! Messenger. La posibilidad de Microsoft de proporcionar este servicio depende de la compatibilidad con Yahoo!, cuyo contrato subyacente está llegando a su fin.</p></li>
<li><p>Hoy más que nunca, Lync es una herramienta eficaz para conectarse dentro de una organización y con individuos de todo el mundo. La federación con Windows Live Messenger no requiere ninguna licencia de usuario o dispositivo adicional aparte de la CAL estándar de Lync. La federación con Skype se agregará a esta lista, lo que permitirá a los usuarios de Lync conectarse con cientos de millones de personas a través de mensajería instantánea y voz.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Cmdlets de servidor perimetral

A continuación se presenta una lista de cmdlets directamente relacionados con la administración de servidores perimetrales:

**Servidor perimetral**

  -   
    [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  -   
    [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  -   
    [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  -   
    [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  -   
    [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  -   
    [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  -   
    [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  -   
    [Set-CsEdgeServer](set-csedgeserver.md)

## Vea también

#### Otros recursos

[Blog de Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150)

