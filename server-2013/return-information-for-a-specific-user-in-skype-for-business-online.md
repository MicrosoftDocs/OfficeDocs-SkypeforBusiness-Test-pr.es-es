---
title: Obtener información sobre un usuario específico
TOCTitle: Obtener información sobre un usuario específico
ms:assetid: 6c8c2190-8e62-4f92-bbe9-4f692bd7ebf5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362803(v=OCS.15)
ms:contentKeyID: 56271318
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtener información sobre un usuario específico

 

_**Última modificación del tema:** 2015-06-22_

Existen varias formas de hacer referencia a una cuenta de usuario concreta al llamar al cmdlet [Get-CsOnlineUser](get-csonlineuser.md). Puede usar el nombre para mostrar de los Servicios de dominio de Active Directory:

    Get-CsOnlineUser -Identity "Ken Myer"

Puede usar la dirección SIP del usuario:

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

Puede usar el nombre principal de usuario del usuario (UPN):

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

