---
title: Error de importación de módulo ocasionado por la directiva de ejecución de Windows PowerShell
TOCTitle: Error de importación de módulo ocasionado por la directiva de ejecución de Windows PowerShell
ms:assetid: 4bc093ca-fd30-44c9-a0a3-16f78698df2b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362786(v=OCS.15)
ms:contentKeyID: 56271283
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Error de importación de módulo ocasionado por la directiva de ejecución de Windows PowerShell

 

_**Última modificación del tema:** 2016-12-08_

La directiva de ejecución de Windows PowerShell ayuda a determinar qué archivos de configuración se pueden subir a la consola de Windows PowerShell y qué scripts puede ejecutar un usuario desde la consola. Como mínimo, el módulo del conector de Skype Empresarial Online no se puede importar a menos que la directiva de ejecución se haya establecido en RemoteSigned. Si no es el caso, verá el mensaje de error siguiente cuando trate de importar el módulo:

    Import-Module : No se puede cargar el archivo C:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnectorStartup.psm1 porque la ejecución de scripts está deshabilitada en el sistema.Para obtener más información, vea about_Execution_Policies en http://go.microsoft.com/fwlink/?LinkID=135170.

Para resolver el problema, inicie Windows PowerShell como administrador y luego ejecute el comando siguiente:

    Set-ExecutionPolicy RemoteSigned

Para más información sobre la directiva de ejecución, vea el tema de Ayuda en [http://go.microsoft.com/fwlink/?LinkID=135170](http://go.microsoft.com/fwlink/?linkid=135170).

## Vea también

#### Conceptos

[Diagnosticar y resolver los problemas de conexión con Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

