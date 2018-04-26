---
title: Cmdlets de enrutamiento estático
TOCTitle: Cmdlets de enrutamiento estático
ms:assetid: 71d5e0cd-8412-4383-818a-95b851a4da4b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg416492(v=OCS.15)
ms:contentKeyID: 48275658
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets de enrutamiento estático

 

_**Última modificación del tema:** 2016-12-08_

Las rutas estáticas permiten que los administradores puedan predeterminar las rutas de red que toman los mensajes SIP. Cuando un servidor recibe un mensaje, comprueba la dirección del mensaje y, a continuación, lo reenvía al servidor del siguiente salto que haya preconfigurado un administrador. Si se configuran correctamente, las rutas estáticas ayudan a asegurar la entrega precisa y puntual de los mensajes sin apenas sobrecargar los servidores.

## Cmdlets de enrutamiento estático

A menos que el personal de soporte técnico de Microsoft indique otra cosa, las rutas estáticas configuradas para Microsoft Lync Server 2013 deben crearse con el cmdlet [New-CsStaticRoute](new-csstaticroute.md). Una vez creada una ruta, los cmdlets CsStaticRoutingConfiguration son aptos para agregar dicha ruta a una recopilación de rutas estáticas.

**Rutas estáticas**

  -   
    [Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)

  -   
    [New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)

  -   
    [Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

  -   
    [Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

  -   
    [New-CsStaticRoute](new-csstaticroute.md)

  -   
    [Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)

  -   
    [New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)

  -   
    [Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

  -   
    [Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

  -   
    [New-CsSipProxyCustom](new-cssipproxycustom.md)

  -   
    [New-CsSipProxyRealm](new-cssipproxyrealm.md)

  -   
    [New-CsSipProxyTCP](new-cssipproxytcp.md)

  -   
    [New-CsSipProxyTLS](new-cssipproxytls.md)

  -   
    [New-CsSipProxyTransport](new-cssipproxytransport.md)

  -   
    [New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

  -   
    [New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

  -   
    [New-CsIssuedCertId](new-csissuedcertid.md)

## Vea también

#### Otros recursos

[Blog de Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0xc0a)

