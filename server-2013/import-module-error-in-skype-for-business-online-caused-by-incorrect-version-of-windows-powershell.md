---
title: Error de importación de módulo ocasionado por una versión incorrecta de Windows PowerShell
TOCTitle: Error de importación de módulo ocasionado por una versión incorrecta de Windows PowerShell
ms:assetid: 6c209f41-2b97-4dda-b0b7-e5b582d3e6b6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362802(v=OCS.15)
ms:contentKeyID: 56271316
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Error de importación de módulo ocasionado por una versión incorrecta de Windows PowerShell

 

_**Última modificación del tema:** 2015-06-22_

El módulo del conector de Skype Empresarial Online solo se puede ejecutar en Windows PowerShell 3.0. Si intenta importar el módulo con una versión anterior de Windows PowerShell, el proceso de importación fallará y verá un mensaje de error parecido a este:

    Import-Module : La versión del PowerShell cargado es "2.0". El módulo 'D:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnector.psd1' requiere como mínimo la versión de PowerShell "3.0" para ejecutarse. Verifique la instalación del PowerShell e inténtelo de nuevo.

La única forma de arreglar el problema es instalar Windows PowerShell 3.0, disponible en el Centro de descarga de Microsoft, en <http://www.microsoft.com/en-us/download/details.aspx?id=29939>.

## Vea también

#### Conceptos

[Diagnosticar y resolver los problemas de conexión con Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

