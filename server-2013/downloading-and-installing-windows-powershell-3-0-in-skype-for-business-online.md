---
title: 'Lync Online: Descargar e instalar Windows PowerShell 3.0'
TOCTitle: Descargar e instalar Windows PowerShell 3.0
ms:assetid: 39ae065d-02d7-4ce3-9e6f-6ad550a1777e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362783(v=OCS.15)
ms:contentKeyID: 56271277
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Descargar e instalar Windows PowerShell 3.0 en Lync Online

 

_**Última modificación del tema:** 2016-12-08_

Si usa Windows Server 2012, Windows Server 2012 R2, Windows 8 o Windows 8.1, ya debería tener Windows PowerShell 3.0, ya que esta aplicación preinstalada con estos sistemas operativos.

Si usa Windows 7 o Windows Server 2008 R2, debería usar Windows PowerShell 3.0. Sin embargo, es posible que esté usando la versión 2.0, que es la versión que se entrega con esos sistemas operativos. Para saber qué versión usa de Windows PowerShell, siga los siguientes pasos en su equipo con Windows 7 o Windows Server 2008 R2:

1.  Haga clic en **Inicio**, Todos los programas, **Accesorios**, **Windows PowerShell** y **Windows PowerShell**.

2.  En la consola de Windows PowerShell, escriba el comando siguiente y presione ENTRAR:
    
        Get-Host | Select-Object Version

3.  En la ventana de la consola, deberá verse una información parecida a la siguiente:
    
        Version
        -------
        3.0

Si el número de versión devuelto es 3.0, significa que está ejecutando Windows PowerShell 3.0. Si el número de versión devuelto no es 3.0, tendrá que instalar Windows PowerShell 3.0. Puede descargar Windows Management Framework 3.0, que incluye Windows PowerShell 3.0, desde el [Centro de descarga de Microsoft](http://www.microsoft.com/en-us/download/details.aspx?id=34595).

Después de comprobar que Windows PowerShell 3.0 esté instalado, tiene que asegurarse de que Windows PowerShell se haya configurado para ejecutar scripts remotos. Para ello, inicie Windows PowerShell como administrador. En Windows 7, Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2 haga lo siguiente:

1.  Haga clic en **Inicio**, **Todos los programas**, **Accesorios** y **Windows PowerShell**, luego haga clic con el botón secundario en **Windows PowerShell** y, por último, haga clic en **Ejecutar como administrador**.

2.  Si aparece el cuadro de diálogo **Control de cuentas de usuario**, haga clic en **Sí** para confirmar que quiere ejecutar Windows PowerShell con las credenciales de administrador.

Si tiene Windows 8, haga esto:

1.  Acceda a la barra de símbolos, haga clic en **Buscar** y haga clic con el botón secundario en **Windows PowerShell**. Puede acceder rápidamente a la barra de símbolos en cualquier PC con Windows 8 (con o sin pantalla táctil) manteniendo presionadas la tecla Windows y la tecla C.

2.  En la barra de herramientas de la parte inferior de la pantalla, haga clic en **Ejecutar como administrador**.

3.  Si aparece el cuadro de diálogo **Control de cuentas de usuario**, haga clic en **Sí** para confirmar que quiere ejecutar Windows PowerShell con las credenciales de administrador.

Cuando se esté ejecutando Windows PowerShell, tendrá que cambiar la directiva de ejecución para permitir que se ejecuten scripts remotos. En la consola de Windows PowerShell, escriba el comando siguiente y presione ENTRAR:

    Set-ExecutionPolicy RemoteSigned -Force


> [!NOTE]
> Al ejecutar el comando anterior, puede que vea el mensaje de error siguiente:<BR>Set-ExecutionPolicy: acceso denegado a la clave del registro 'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Micrsoft.PowerShell'.<BR>Este mensaje de error suele aparecer cuando no se está ejecutando Windows PowerShell con credenciales de administrador. Cierre la sesión de Windows PowerShell e inicie otra nueva como administrador.



Para comprobar si la directiva de ejecución se ha configurado bien, escriba lo siguiente en el símbolo del sistema de Windows PowerShell y presione ENTRAR:

    Get-ExecutionPolicy

Si recibe el valor siguiente, quiere decir que todo se ha configurado correctamente:

    RemoteSigned

Si actualmente no usa Windows PowerShell 3.0, también tendrá que descargar e instalar Windows Management Framework 3.0 del Centro de descarga de Microsoft. Se trata de un paquete de instalación que incluye Windows PowerShell 3.0 y Administración remota de Windows (WinRM) 3.0. Este paquete de instalación puede ser necesario si usa Windows 7 y todavía no ha actualizado a Windows PowerShell 3.0. Si está utilizando Windows Server 2012, Windows Server 2012 R2, Windows 8 o Windows 8.1, no debería ser necesario instalar Windows PowerShell 3.0. Windows PowerShell 3.0 viene preinstalado en estos sistemas operativos.

Antes de instalar Windows Management Framework 3.0:

  - Asegúrese de haberse bajado la versión correcta del paquete de instalación. Si usa la versión de 64 bits de Windows 7, bájese el archivo Windows6.1-KB2506143-x64.msu. Si usa la versión de 32 bits de Windows 7, bájese el archivo Windows6.1-KB2506143-x86.msu.

  - Si usa Windows 7 en el PC, asegúrese de que tiene instalado Windows 7 Service Pack 1.

Si no sabe con certeza la versión de Windows que tiene o no sabe si tiene instalado Windows 7 Service Pack 1, haga clic en **Inicio**, haga clic con el botón secundario en **Equipo** y luego haga clic en **Propiedades**. Esta información aparecerá en el cuadro de diálogo del sistema:

![Cuadro de diálogo del sistema con las opciones de configuración](images/Dn362783.30bff2e8-2862-4dd7-828f-43732f4b9314(OCS.15).png "Cuadro de diálogo del sistema con las opciones de configuración")

Para instalar Windows Management Framework 3.0, siga estos pasos:

1.  Haga doble clic en el archivo de instalación .MSU ( **Windows6.1-KB2506143-x64.msu** o **Windows6.1-KB2506143-x86.msu**).

2.  En el Asistente para descargar e instalar actualizaciones, en la página **Lea los términos de la licencia (1 de 1)**, haga clic en **Acepto**.

3.  Cuando se complete la instalación, haga clic en **Reiniciar ahora** para reiniciar el PC.

Después de reiniciar el PC, compruebe que Windows PowerShell se pueda iniciar y que la aplicación se pueda ejecutar con credenciales administrativas. Para ello:

1.  Haga clic en **Inicio**, **Todos los programas**, **Accesorios** y **Windows PowerShell**, luego haga clic con el botón secundario en **Windows PowerShell** y, por último, haga clic en **Ejecutar como administrador**.

2.  Si aparece el cuadro de diálogo Control de cuentas de usuario, haga clic en **Sí** para confirmar que quiere ejecutar Windows PowerShell con las credenciales de administrador.

Cuando aparezca la consola de Windows PowerShell, deberá comprobar si el servicio WinRM se está ejecutando y está bien configurado. Para saber si el servicio se está ejecutando, escriba el comando siguiente en el símbolo del sistema de Windows PowerShell y presione ENTRAR:

    Get-Service winrm

En la pantalla, aparecerá información sobre el servicio WinRM:

    Status   Name               DisplayName
    ------   ----               -----------
    Running  winrm              Windows Remote Management (WS-Manag...

Si el estado del servicio no es "En ejecución", inicie el servicio WinRM escribiendo el comando siguiente y luego presione ENTRAR:

    Start-Service winrm

Tras iniciar el servicio, ejecute el comando siguiente para asegurarse de que WinRM use la autenticación básica:

    winrm set winrm/config/client/auth '@{Basic="True"}'

En la pantalla se verá una información parecida a la siguiente:

    Auth
        Basic = true
        Digest = true
        Kerberos = true
        Negotiate = true
        Certificate = true
        CredSSP = false

Si la autenticación básica se ha establecido en "true", ya puede usar Windows PowerShell para conectarse a Skype Empresarial Online.

