---
title: Obtener información específica para usuarios específicos
TOCTitle: Obtener información específica para usuarios específicos
ms:assetid: bbee85bd-d8a7-4b28-90d7-45c43eee48f6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362838(v=OCS.15)
ms:contentKeyID: 56271345
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener información específica para usuarios específicos

 

_**Última modificación del tema:** 2015-06-22_

De forma predeterminada, el cmdlet [Get-CsOnlineUser](get-csonlineuser.md) devuelve una gran cantidad de información para cada cuenta de usuario de Skype Empresarial Online. Si solo le interesa un subconjunto de esa información, canalice los datos devueltos al cmdlet **Select-Object**. Por ejemplo, este comando devuelve todos los datos del usuario Ken Myer y luego usa el cmdlet **Select-Object** para limitar la información que se muestra en pantalla a solo el plan de marcado y el nombre para mostrar de Servicios de dominio de Active Directory de Ken:

    Get-CsOnlineUser -Identity "Ken Myer" | Select-Object DisplayName, DialPlan

El siguiente comando devuelve el plan de marcado y el nombre para mostrar de todos los usuarios.

    Get-CsOnlineUser | Select-Object DisplayName, DialPlan

Para buscar las propiedades de una cuenta de usuario de Skype Empresarial Online, use este comando:

    Get-CsOnlineUser | Get-Member

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

