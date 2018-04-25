---
title: 'Lync Online: los cmdlet de informes de Lync Online y el servicio web REST'
TOCTitle: Los cmdlet de informes de Lync Online y el servicio web REST
ms:assetid: cadd73a7-c08a-4102-b73a-ccb3ad4987bf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362845(v=OCS.15)
ms:contentKeyID: 56271354
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Los cmdlet de informes de Lync Online y el servicio web REST

 

_**Última modificación del tema:** 2016-12-08_

Junto con las características de informes, Skype Empresarial Online ofrece acceso a cinco cmdlets Windows PowerShell que facilitan la generación de los informes y que los administradores pueden usar para devolver datos de informes personalizados. Skype Empresarial Online también incluye la transferencia de estado de representación (REST). Solo los desarrolladores pueden usarla para recuperar información de informes personalizada.

Los cmdlets de informes disponibles para los administradores son los siguientes:

  - Get-CsActiveUserReport: información sobre el número de usuarios activos (usuarios que han iniciado sesión en Skype Empresarial Online y han participado como mínimo en una sesión de comunicación de punto a punto o en una conferencia).

  - Get-CsAVConferenceTimeReport: información sobre la cantidad de tiempo (en minutos) que los usuarios han empleado en conferencias de audio o vídeo.

  - Get-CsConferenceReport: información sobre el número y el tipo de conferencias en las que han participado los usuarios.

  - Get-CsP2PAVTimeReport: información sobre la cantidad de tiempo (en minutos) que los usuarios han empleado en sesiones de punto a punto con audio o vídeo.

  - Get-CsP2PSessionReport: información sobre el número y el tipo de sesiones de punto a punto en las que han participado los usuarios.

La mayoría de los administradores usará los informes disponibles en el Centro de administración de Office 365: estos informes se generan de forma automática y proporcionan una representación gráfica de los datos. A menudo, esta representación es más fácil de interpretar que los valores numéricos sin procesar que devuelven los cmdlets de informes. Sin embargo, los administradores familiarizados con Windows PowerShell pueden usar los cmdlets de informes para devolver datos que no se encuentran fácilmente en los informes de Lync Online. Por ejemplo, los cmdlets de informes devuelven información sobre la duración de las sesiones (los minutos que duró cada sesión). La duración de cada una de las sesiones no está disponible en los informes de Lync Online. Del mismo modo, en la vista diaria, los informes de Lync Online solo muestran información sobre los 14 días anteriores. Para ver los totales diarios de otra fecha (por ejemplo, de hace cuatro meses), puede usar los cmdlets de informes.

También puede resultar interesante para los administradores el artículo [Uso de Excel para recuperar datos de informes de Office 365](http://msdn.microsoft.com/es-es/library/dn781442.aspx), que explica cómo usar la característica de consultas de datos de OData de Microsoft Excel para crear informes personalizados de Office 365. Con los informes personalizados, puede determinar qué datos (y cuántos datos) devolverá el servicio de informes de Office 365. Con los informes personalizados, también puede realizar acciones como, por ejemplo, especificar cómo se deben ordenar y agrupar los datos o proporcionar acceso a información que no se muestra en el Centro de administración de Office 365.

Los administradores en entornos de desarrollo pueden usar el servicio web REST para obtener información que no aparece en el Centro de administración de Skype Empresarial Online. Este servicio es similar al servicio SOAP, en cuanto a que ambos tipos de tecnología permiten transferir datos XML entre un cliente y un servidor. No obstante, el servicio REST tiene al menos dos ventajas en comparación con el servicio SOAP. En primer lugar, REST realiza las transferencias de datos XML con un formato estandarizado denominado formato para redifusión web ATOM. Por el contrario, el formato de transferencia de datos de SOAP no es estándar. Además, REST puede transferir datos a través de redes que bloquean los verbos HTTP distintos de GET y POST.

## Vea también

#### Otros recursos

[Informes de Lync Online](https://technet.microsoft.com/es-es/library/dn362827\(v=ocs.15\))  
[Servicio Web de informes de Office 365](http://msdn.microsoft.com/es-es/library/office/jj984325.aspx)  
[Aprendizaje acerca del servicio web de informes de Office 365](http://msdn.microsoft.com/es-es/library/office/jj984321.aspx)  
[Cmdlets de informes de Exchange Online](http://technet.microsoft.com/es-es/library/jj200780\(v=exchg.150\).aspx)  
[Uso de Excel para recuperar datos de informes de Office 365](http://msdn.microsoft.com/es-es/library/dn781442.aspx)

