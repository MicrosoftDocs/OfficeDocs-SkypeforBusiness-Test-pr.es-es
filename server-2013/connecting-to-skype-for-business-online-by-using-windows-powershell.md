---
title: Conectar con Lync Online mediante Windows PowerShell
TOCTitle: Conectar con Lync Online mediante Windows PowerShell
ms:assetid: 6167dad9-9628-4fdb-bed1-bdb3f7108e64
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362795(v=OCS.15)
ms:contentKeyID: 56271306
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Conectar con Lync Online mediante Windows PowerShell

 

_**Última modificación del tema:** 2017-03-03_

Una vez instalado el software de los requisitos previos, ya puede empezar a usar Windows PowerShell para administrar Skype Empresarial Online. Para ello, abra una instancia estándar de Windows PowerShell. No hay que abrir una instancia especial de Windows PowerShell (se parece, en cierto modo, al Shell de administración de Lync Server), ninguna aplicación del panel de control ni ningún otro tipo especial de aplicación, ya que la administración de Skype Empresarial Online se lleva a cabo usando una sesión remota de Windows PowerShell. Esto significa que:

1.  Se usa una sesión normal de Windows PowerShell para conectarse a Skype Empresarial Online. Al conectarnos remotamente, trabajamos en el PC local y usamos la copia local de Windows PowerShell, pero administramos los objetos encontrados en un sistema remoto (es decir, Skype Empresarial Online).

2.  Todos los cmdlets, scripts y elementos necesarios para administrar Skype Empresarial Online se bajan a su PC. Estos elementos se guardan en la memoria y solo están disponibles en la sesión remota establecida con Skype Empresarial Online. Es importante recordar esto: al establecer una conexión remota con Skype Empresarial Online, los cmdlets de Skype Empresarial Online, como [Get-CsTenant](get-cstenant.md), se copiarán a la memoria del PC. Estos cmdlets los podrá ejecutar únicamente en la sesión remota. Puede iniciar una segunda sesión de Windows PowerShell, por ejemplo, pero sin conectarse a Skype Empresarial Online en ella. Si intenta ejecutar el cmdlet **Get-CsTenant** en esta sesión, verá el mensaje de error siguiente:
    
        Get-CsTenant : The term 'Get-CsTenant' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
    
    Además, si busca en el disco duro el cmdlet **Get-CsTenant** (o cualquier otro cmdlet de Skype Empresarial Online), no encontrará nada, ya que, en realidad, no se guarda nada en el disco duro al crear una sesión remota.

3.  Al cerrar la sesión remota, los elementos bajados se eliminan de la memoria del PC. Por ejemplo, puede empezar una sesión remota de Windows PowerShell con el cmdlet **Get-CsTenant** y luego cerrarla. Si reinicia Windows PowerShell, el cmdlet **Get-CsTenant** ya no estará disponible. Para acceder al cmdlet **Get-CsTenant**, tendrá que volver a conectarse con Skype Empresarial Online.


> [!NOTE]
> Si está trabajando con una implementación híbrida, debe seguir los procedimientos que se describen en el artículo <A href="using-windows-powershell-in-a-hybrid-deployment-with-skype-for-business-online.md">Usar Windows PowerShell en implementaciones híbridas</A>.



Para crear una conexión remota con Skype Empresarial Online, inicie una sesión nueva de Windows PowerShell on your local computer. Si tiene Windows 7, Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2 haga lo siguiente:

  - Haga clic en **Inicio**, **Todos los programas**, **Accesorios**, **Windows PowerShell** y **Windows PowerShell**.

Si tiene Windows 8 u 8.1, haga esto:

  - Acceda a la barra de símbolos, haga clic en **Buscar** y en **Windows PowerShell**. Puede acceder rápidamente a la barra de símbolos en cualquier PC con Windows 8 u 8.1 (con o sin pantalla táctil) manteniendo presionada la tecla Windows y presionando la tecla C.

Cuando aparezca la consola de Windows PowerShell, debe crear un objeto de credenciales de Windows PowerShell. El objeto de credenciales se usa para transmitir con seguridad su nombre de usuario y contraseña a Skype Empresarial Online. Para crear un objeto de credenciales, escriba el comando siguiente en el símbolo del sistema de Windows PowerShell y presione ENTRAR:

    $credential = Get-Credential


> [!NOTE]
> En este ejemplo, el nombre de usuario y la contraseña se almacenarán en la variable $credential. Puede ponerle cualquier nombre a esta variable siempre que cumpla las reglas de los nombres de variable de Windows PowerShell, pero tiene que usar una variable de algún tipo para almacenar el nombre de usuario y la contraseña. De lo contrario, el objeto de credenciales que cree desaparecerá nada más crearse.



Después de presionar ENTRAR, debería ver el cuadro de diálogo **Credencial de Windows PowerShell**:

![Credenciales de inicio de sesión en Windows PowerShell](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Credenciales de inicio de sesión en Windows PowerShell")

En el cuadro **Nombre de usuario**, escriba el nombre de usuario de Skype Empresarial Online. En el cuadro **Contraseña**, escriba la contraseña de Skype Empresarial Online (esta se enmascarará y no se verá en la pantalla). Por ejemplo, si el nombre de usuario es kenmyer@litwareinc.com y la contraseña es p@ssw0rd\!, en el cuadro de diálogo se verá esto:

![Credenciales de inicio de sesión en Windows PowerShell](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Credenciales de inicio de sesión en Windows PowerShell")

Para crear el objeto de credenciales, haga clic en **Aceptar**. Si quiere comprobar si se ha creado el objeto, escriba el nombre de la variable en el símbolo del sistema de Windows PowerShell y presione ENTRAR:

    $credential

Windows PowerShell responderá mostrando algo como esto:

    UserName                            Password
    --------                            --------
    kenmyer@litwareinc.com              System.Security.SecureString


> [!NOTE]
> Recuerde que el cmdlet <STRONG>Get-Credential</STRONG> acepta cualquier credencial que escriba y que no se encarga de comprobar si el nombre de usuario y la contraseña que ha introducido son válidos. Esta validación solo se hará cuando intente iniciar sesión en Skype Empresarial Online.



Después de crear el objeto de credenciales, puede crear una nueva sesión remota de Windows PowerShell que establezca una conexión con Skype Empresarial Online. Para ello, escriba el comando siguiente en el símbolo del sistema de Windows PowerShell y presione ENTRAR:

    $session = New-CsOnlineSession -Credential $credential


> [!NOTE]
> $session es una variable que se usa para retener información (en este caso, información sobre la conexión con Skype Empresarial Online). A esta variable también le puede poner cualquier nombre siempre que cumpla las instrucciones de nombres de variable de Windows PowerShell (por ejemplo, no incluir espacios en blanco ni signos de puntuación).



Asegúrese de escribir el comando tal y como aparece (con la posible excepción del nombre de la variable). Da igual cuál sea el nombre de su dominio de Skype Empresarial Online. Independientemente del nombre del dominio, el cmdlet **New-CsOnlineSession** le conectará con Office 365 para que inicie sesión con las credenciales indicadas. Después de establecer la conexión y haberse autenticado, se le redirigirá automáticamente al URI apropiado según las credenciales facilitadas.

Si la conexión se establece correctamente, verá mensajes parecidos a este en la consola de Windows PowerShell:

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

¿Ya puede empezar a usar Windows PowerShell para administrar Skype Empresarial Online? Todavía no. El cmdlet **New-CsOnlineSession** se conecta con Skype Empresarial Online y le crea una sesión nueva que tendrá que importar a la consola de Windows PowerShell. Para hacerlo, ejecute el comando siguiente:

    Import-PSSession $session

Cuando presione ENTRAR, en la consola de Windows PowerShell verá un indicador de progreso parecido a este:

    Creating implicit remoting module . . .
         Getting command information from remote session . . . 16 commands  
              received
         [oooooooooooooooo
         00:00:33 remaining

Lo que está pasando ahora es que Windows PowerShell está bajando cmdlets y otros elementos necesarios para administrar Skype Empresarial Online. Cuando termine la descarga, verá una información como la que aparece a continuación en la consola de Windows PowerShell:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enable-Cs ...}

Ahora ya puede empezar a usar Windows PowerShell para administrar Skype Empresarial Online. Para comprobar si la descarga se ha realizado correctamente y ver qué cmdlets de Skype Empresarial Online se pueden usar, primero tiene que determinar el nombre del módulo temporal de Windows PowerShell que contiene todos los cmdlets de Skype Empresarial Online. Para hacerlo, ejecute este comando desde el símbolo del sistema de Windows PowerShell:

    Get-Module

En la pantalla se verá una información parecida a la siguiente:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

El módulo que tiene el script ModuleType es el que contiene los cmdlets de Skype Empresarial Online. Para devolver una lista de estos cmdlets, ejecute el cmdlet **Get-Command** usando el nombre del módulo de script como nombre del módulo:

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell debería mostrar una lista con todos los cmdlets de Skype Empresarial Online.

Cuando termine las tareas de administración, siempre tiene que ejecutar el comando siguiente antes de cerrar la consola de Windows PowerShell:

    Remove-PSSession $session

El cmdlet **Remove-PSSession** lo desconecta de Skype Empresarial Online y cierra la sesión remota. De hecho, si intenta volver a importar la sesión (ejecutando el cmdlet **Import-PSSession**), verá el siguiente mensaje de error:

    Import-PSSession : State of runspace is not valid for this operation.

Este mensaje quiere decir que, para volver a conectarse con Skype Empresarial Online, tiene que crear una sesión nueva.

Si se olvida de quitar la sesión antes de cerrar la consola de Windows PowerShell (o si la consola se cierra inesperadamente), no pasa nada. Después de 15 minutos de inactividad, la sesión se desconectará automáticamente. Sin embargo, de manera predeterminada, un administrador de Skype Empresarial Online solo puede establecer tres conexiones simultáneas con Skype Empresarial Online. Si cierra la consola de Windows PowerShell sin quitar la sesión, la sesión cerrada seguirá contando como una conexión aunque no se está usando en ese momento. (Y seguirá contándose como una conexión hasta que se agote el tiempo de espera). Supongamos, por ejemplo, que abre y cierra la consola de Windows PowerShell tres veces sin quitar la sesión de Skype Empresarial Online ninguna de las veces. Si abre Windows PowerShell e intenta establecer una cuarta conexión, el comando se colgará y no se hará ninguna conexión.


> [!NOTE]
> Si Windows PowerShell se cuelga al intentar hacer una conexión, presione Ctrl-C para cerrar el comando bloqueado.



Aunque los administradores pueden tener solo tres conexiones simultáneas con un inquilino de Skype Empresarial Online, una organización puede establecer hasta nueve conexiones a la vez. Esto significa que, entre otras posibilidades, tres administradores podrían tener tres conexiones simultáneas cada uno o que nueve administradores podrían tener una conexión con Skype Empresarial Online. En cualquier caso, ningún administrador puede tener más de tres sesiones activas.

## Vea también

#### Conceptos

[Configurar el equipo para la administración de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

