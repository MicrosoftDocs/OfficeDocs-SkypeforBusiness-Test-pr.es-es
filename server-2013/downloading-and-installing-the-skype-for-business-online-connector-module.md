---
title: Descargar e instalar el módulo del conector de Lync Online
TOCTitle: Descargar e instalar el módulo del conector de Lync Online
ms:assetid: a0c87219-b642-4201-85d4-a85c2163d1eb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362829(v=OCS.15)
ms:contentKeyID: 56271343
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Descargar e instalar el módulo del conector de Lync Online

 

_**Última modificación del tema:** 2016-12-08_

El módulo del conector de Skype Empresarial Online incluye el cmdlet **New-CsOnlineSession**, que le permite crear una sesión de Windows PowerShell remota que se conecte a Skype Empresarial Online. Este módulo, que solo se admite en equipos de 64 bits (consulte [Configurar el equipo para la administración de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md) para más información), se puede descargar desde el Centro de descarga de Microsoft en [http://go.microsoft.com/fwlink/?LinkId=294688](http://go.microsoft.com/fwlink/?linkid=294688). Descargue el archivo LyncOnlinePowershell.exe y luego complete el siguiente procedimiento:

1.  Haga doble clic en el archivo **LyncOnlinePowershell.exe**.

2.  En el asistente para la instalación de PowerShell de inquilinos de Skype Empresarial Online, en la página **Microsoft Software License Terms**, seleccione **I accept the terms in the License Agreement** y luego haga clic en **Install**. Si aparece el cuadro de diálogo **User Account Control**, haga clic en **Yes** para continuar con la instalación.

3.  En la página que indica que se **Completed the Microsoft Lync Online, Tenant PowerShell Setup**, haga clic en **Finish**.

El programa de instalación copia el módulo del conector de Skype Empresarial Online (y el cmdlet **New-CsOnlineSession**) en el equipo local. Para acceder al módulo, inicie una sesión de Windows PowerShell con credenciales de administrador y luego ejecute el siguiente comando:

    Import-Module LyncOnlineConnector

Si no quiere escribir este comando cada vez que inicie Windows PowerShell, puede agregarlo al perfil de Windows PowerShell. Para ello, escriba el siguiente comando en el símbolo del sistema de Windows PowerShell y presione ENTRAR:

    notepad.exe $profile

Cuando aparezca el Bloc de notas, agregue la siguiente línea después de los comandos que ya están en el perfil (si hay alguno):

    Import-Module LyncOnlineConnector

Guarde el archivo. La próxima vez que inicie Windows PowerShell, el módulo del conector de Skype Empresarial Online se importará automáticamente. Tenga en cuenta que recibirá un mensaje de error y no se cargará el módulo si no ejecuta Windows PowerShell con credenciales de administrador.

Además de instalar el módulo del conector de Skype Empresarial Online, LyncOnlinePowershell.exe también instala dos componentes adicionales: .NET Framework 4.5 y el paquete redistribuible de Microsoft Visual C++ 2012 (x64; versión 11.0.50727). .NET Framework 4.5 proporciona la infraestructura que se usa para compilar y ejecutar aplicaciones de .NET, incluido Windows PowerShell. El paquete redistribuible de Visual C++ instala los componentes de tiempo de ejecución de Visual C++ en equipos que no tienen instalado Microsoft Visual Studio 2012.

## Vea también

#### Conceptos

[Configurar el equipo para la administración de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

