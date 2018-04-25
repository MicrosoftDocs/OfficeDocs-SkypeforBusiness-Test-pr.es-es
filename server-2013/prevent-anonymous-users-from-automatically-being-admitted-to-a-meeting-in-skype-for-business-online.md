---
title: Impedir la admisión automática de los usuarios anónimos en las reuniones
TOCTitle: Impedir la admisión automática de los usuarios anónimos en las reuniones
ms:assetid: 23f120d2-4c39-4509-aa1f-4d186a525075
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362775(v=OCS.15)
ms:contentKeyID: 56271273
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impedir la admisión automática de los usuarios anónimos en las reuniones

 

_**Última modificación del tema:** 2015-06-22_

Para impedir que los usuarios anónimos se admitan automáticamente en una reunión en línea, use el cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) y establezca la propiedad AdmitAnonymousUsersByDefault en False ($False):

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

Para habilitar la admisión automática, vuelva a establecer la propiedad AdmitAnonymousUsersByDefault en True ($True):

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $True

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

