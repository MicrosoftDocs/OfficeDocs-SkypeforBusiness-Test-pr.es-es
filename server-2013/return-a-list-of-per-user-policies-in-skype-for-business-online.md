---
title: Obtener una lista de las directivas por usuario
TOCTitle: Obtener una lista de las directivas por usuario
ms:assetid: e95a2755-3501-40cc-a704-5ecd01839d76
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362856(v=OCS.15)
ms:contentKeyID: 56271369
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener una lista de las directivas por usuario

 

_**Última modificación del tema:** 2015-06-22_

Para obtener una lista de las directivas disponibles por usuario, seleccione en primer lugar el cmdlet **Get-Cs** adecuado (por ejemplo, el cmdlet [Get-CsVoicePolicy](get-csvoicepolicy.md) para obtener las directivas de voz por usuario). A continuación, use la sintaxis siguiente para obtener el parámetro Identity de las distintas directivas por usuario:

    Get-CsVoicePolicy -Filter "tag:*" | Select-Object Identity

Tenga en cuenta que, debido a los distintos contratos de licencia y las restricciones del país o la región, es posible que no pueda asignar ciertas directivas de conferencia, acceso externo o movilidad a un usuario en particular. Para comprobar las directivas por usuario que sí puede asignar a un usuario determinado (por ejemplo, kenmyer@litwareinc.com), use uno de los comandos siguientes (con el parámetro ApplicableTo), según proceda:

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

La sintaxis anterior solo devuelve las directivas por usuario que sí pueden asignarse a Ken Myer.

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

