---
title: Error de conexión con el servidor de Live ID
TOCTitle: Error de conexión con el servidor de Live ID
ms:assetid: 701af721-dd6a-4f48-96f9-94e89c644201
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362811(v=OCS.15)
ms:contentKeyID: 56271321
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Error de conexión con el servidor de Live ID

 

_**Última modificación del tema:** 2015-06-22_

Existen tres razones comunes por las que un intento de conexión puede fallar y generar este mensaje de error:

    Get-CsWebTicket : Error al conectar a los servidores de Live ID. Asegúrese de que el proxy esté habilitado o que la máquina disponga de conexión de red a los servidores de Live ID.

A menudo, este error quiere decir que Microsoft Online Services - Ayudante para el inicio de sesión no está ejecutándose. Puede comprobar el estado de este servicio ejecutando el comando siguiente desde el símbolo del sistema de Windows PowerShell:

    Get-Service "msoidsvc"

Si el servicio no se está ejecutando, inícielo con este comando:

    Start-Service "msoidsvc"

Si se está ejecutando, puede que haya problemas con la conexión de red entre el PC y el servidor de autenticación de Microsoft Live ID. Para comprobarlo, abra Internet Explorer y vaya a <https://login.microsoftonline.com/.> Intente iniciar sesión en Office 365 desde aquí. Si no funciona, es probable que haya problemas de conexión de red.

Aunque es menos común, es posible que el URI de conexión del servidor de autenticación de Microsoft Live ID se haya configurado con un valor incorrecto. Si ya ha comprobado que el Ayudante para el inicio de sesión se está ejecutando y que no hay problemas de conectividad de red, puede que sea este el problema. Si es el caso, póngase en contacto con el soporte técnico de Office 365.

## Vea también

#### Conceptos

[Diagnosticar y resolver los problemas de conexión con Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

