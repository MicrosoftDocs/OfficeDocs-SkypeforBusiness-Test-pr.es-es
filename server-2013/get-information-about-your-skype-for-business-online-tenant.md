---
title: Obtener información sobre un inquilino de Lync Online
TOCTitle: Obtener información sobre un inquilino de Lync Online
ms:assetid: 06467515-9114-45bb-8d09-26a915c3fc4d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362768(v=OCS.15)
ms:contentKeyID: 56271262
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener información sobre un inquilino de Lync Online

 

_**Última modificación del tema:** 2015-06-22_

Para devolver información sobre su inquilino de Skype Empresarial Online, llame al cmdlet [Get-CsTenant](get-cstenant.md) sin parámetros adicionales:

    Get-CsTenant

Para devolver solo el identificador y el nombre del inquilino (el valor del parámetro TenantID es obligatorio al ejecutar cmdlets como [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) y [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)), use este comando:

    Get-CsTenant | Select-Object Name, TenantID

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

