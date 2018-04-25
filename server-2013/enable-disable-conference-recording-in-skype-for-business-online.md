---
title: Habilitar o deshabilitar la grabación de conferencias
TOCTitle: Habilitar o deshabilitar la grabación de conferencias
ms:assetid: f6c5afab-081c-495c-97f7-135dcc2f6085
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362857(v=OCS.15)
ms:contentKeyID: 56271374
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Habilitar o deshabilitar la grabación de conferencias

 

_**Última modificación del tema:** 2015-06-22_

Si no desea que los usuarios puedan grabar conferencias en línea, use el cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) y establezca el valor del parámetro AllowConferenceRecording en Falso ($False):

    Set-CsMeetingConfiguration -AllowConferenceRecording $False

Para restaurar la capacidad de grabar conferencias en línea, establezca el valor del parámetro AllowConferenceRecording en Verdadero ($True):

    Set-CsMeetingConfiguration -AllowConferenceRecording $True

## Vea también

#### Conceptos

[Referencia rápida: Realizar tareas de administración comunes de Lync Online con Windows PowerShell](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

