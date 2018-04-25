---
title: Asignar un proveedor de servicios de audioconferencia a un usuario
TOCTitle: Asignar un proveedor de servicios de audioconferencia a un usuario
ms:assetid: 60db6896-9c5c-4d64-ab7e-10d91748587c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362791(v=OCS.15)
ms:contentKeyID: 56271304
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Asignar un proveedor de servicios de audioconferencia a un usuario

 

_**Última modificación del tema:** 2015-06-22_

El cmdlet [Set-CsUserAcp](set-csuseracp.md) es una forma de asignar un proveedor de audioconferencia a un usuario:

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "12065551219" -TollFreeNumbers "18005550712" -ParticipantPasscode "p@ssw0rd" -Domain "sip.contoso.com" -Name "Contoso ACP"

Esta asignación no tendrá valor a menos que haya firmado un contrato con el proveedor indicado.

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

