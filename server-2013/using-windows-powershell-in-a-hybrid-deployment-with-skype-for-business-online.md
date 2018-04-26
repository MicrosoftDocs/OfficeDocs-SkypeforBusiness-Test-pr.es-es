---
title: Usar Windows PowerShell en implementaciones híbridas
TOCTitle: Usar Windows PowerShell en implementaciones híbridas
ms:assetid: b19625d4-4b68-403c-a072-5296aa590556
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362835(v=OCS.15)
ms:contentKeyID: 56271356
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Usar Windows PowerShell en implementaciones híbridas

 

_**Última modificación del tema:** 2015-06-22_

En las implementaciones híbridas, las organizaciones tienen algunos usuarios hospedados en la versión local de Lync Server 2013 y otros, en Skype Empresarial Online. Puede usar una única sesión de Windows PowerShell para administrar de forma simultánea tanto la versión local de Lync Server como el inquilino de Skype Empresarial Online. Para ello, necesitará comprender dos puntos importantes:

1.  Cómo establecer una conexión simultánea a Lync Server y Skype Empresarial Online.

2.  Cómo hacer referencia a la configuración de Skype Empresarial Online desde esta conexión simultánea.

Establecer una conexión simultánea a Lync Server y Skype Empresarial Online es asombrosamente fácil. Para hacerlo, primero conecte Lync Server como lo hace siempre, ya sea iniciando el Shell de administración de Lync Server o creando una conexión remota a un grupo de servidores front-end. Una vez que se haya conectado correctamente a la versión local de Lync Server, podrá conectarse a Skype Empresarial Online tal como si se estuviera conectando solo a Skype Empresarial Online. Para ello, primero debe crear un objeto de credenciales de Windows PowerShell con su información de inicio de sesión de Office 365. Escriba lo siguiente en el símbolo del sistema de Windows PowerShell y luego presione ENTRAR:

    $credential = Get-Credential

Cuando presione ENTRAR, verá el cuadro de diálogo **Credencial de Windows PowerShell**:

![Credenciales de inicio de sesión en Windows PowerShell](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Credenciales de inicio de sesión en Windows PowerShell")

En el cuadro **Nombre de usuario**, escriba su nombre de Skype Empresarial Online. En el cuadro **Contraseña**, escriba su contraseña de Skype Empresarial Online (estará enmascarada y no aparecerá visible en la pantalla). Por ejemplo, si su nombre de usuario es kenmyer@litwareinc.com y su contraseña es p@ssw0rd\!, el cuadro de diálogo será el siguiente:

![Credenciales de inicio de sesión en Windows PowerShell](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Credenciales de inicio de sesión en Windows PowerShell")

Para crear el objeto de credenciales, haga clic en **Aceptar**. Una vez que lo haya creado, puede conectarse a Skype Empresarial Online ejecutando el siguiente comando:

    $session = New-CsOnlineSession -Credential $credential

Asegúrese de escribir el comando tal como se muestra. Tenga en cuenta que no importa cuál es el nombre del dominio de Skype Empresarial Online. El cmdlet **New-CsOnlineSession** lo conectará a Office 365 e iniciará su sesión con las credenciales proporcionadas. Una vez conectado y autenticado, se redirigirá automáticamente al URI correspondiente.

Si la conexión se establece correctamente, verá un mensaje similar a este en la consola de Windows PowerShell:

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

Cuando se conecte a Skype Empresarial Online, importe esa sesión ejecutando un comando similar al siguiente:

    Import-PSSession $session -AllowClobber


> [!NOTE]
> El parámetro AllowClobber se asegura de que se importen todos los cmdlets de Skype Empresarial Online, incluidos los que tienen el mismo nombre que los cmdlets de Lync Server regulares. Serán muchos porque la mayoría de los cmdlets de Skype Empresarial Online, incluidos <A href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</A>, <A href="new-csexumcontact.md">New-CsExUmContact</A>, <A href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</A>, etc., tienen un equivalente local. Los cmdlets emparejados (por ejemplo, <STRONG>Get-CsMeetingConfiguration</STRONG> de Lync Server y <STRONG>Get-CsMeetingConfiguration</STRONG> de Skype Empresarial Online) son idénticos, por lo que no importa cuál se use. El único motivo por el cual se usa el parámetro AllowClobber es para evitar que aparezcan mensajes de advertencia en la pantalla.



Ya está listo para comenzar a administrar tanto la versión local de Lync Server como Skype Empresarial Online. En este momento, puede que también se pregunte cómo diferenciar entre directivas y configuraciones de Lync Server, y directivas y configuraciones de Skype Empresarial Online. Por ejemplo, para cambiar la configuración de reunión global, se ejecuta este comando:

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False

Este comando modifica la configuración global. Pero, ¿qué configuración: la de Lync Server local, la de Skype Empresarial Online, ambas o ninguna?

En este caso en particular, se modificará la configuración local. Lo sabemos porque el parámetro Tenant no se incluyó en el comando. Si está conectado de forma simultánea a Lync Server local y a Skype Empresarial Online, los cmdlets que funcionan en ambas plataformas se ejecutarán en Lync Server, a menos que indique lo contrario. Y el único modo de indicar lo contrario es incluyendo el parámetro Tenant al ejecutar el comando. Por ejemplo, este comando actualiza la configuración global del inquilino de Skype Empresarial Online con identificador bf19b7db-6960-41e5-a139-2aa373474354:

    Set-CsMeetingConfiguration -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AdmitAnonymousUsersByDefault $False

El parámetro Tenant es la clave. Este comando devuelve la directiva de acceso externo global para Lync Server local:

    Get-CsExternalAccessPolicy -Identity "global"

Y este devuelve la directiva de acceso externo global para el inquilino de Skype Empresarial Online:

    Get-CsExternalAccessPolicy -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Tenga en cuenta que hay más de 700 cmdlets locales. Pero la gran mayoría de ellos no tienen el parámetro Tenant, lo que significa que no se pueden usar con Skype Empresarial Online. Además, unos cuantos cmdlets que tienen el parámetro Tenant aún no están disponibles para usarlos con Skype Empresarial Online. Para recuperar el conjunto exacto de cmdlets que pueden usarse con Skype Empresarial Online, ejecute este comando desde el símbolo del sistema de Windows PowerShell:

    Get-Module

En pantalla verá información similar a la siguiente:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

El módulo cuyo ModuleType es Script es el que contiene los cmdlets de Skype Empresarial Online. Para devolver una lista de esos cmdlets, ejecute **Get-Command** usando el nombre del módulo Script como nombre de módulo:

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell mostrará una lista de todos los cmdlets de Skype Empresarial Online.

**Solución de problemas de conexión en una implementación híbrida**

En algunos casos, los administradores pueden experimentar problemas al iniciar sesión en Office 365 cuando se utiliza una cuenta local (por ejemplo, administrator@litwareinc.net) en vez de una cuenta de Office 365 (como administrator@litwareinc.onmicrosoft.com). Si la sincronización de directorios funciona correctamente, debería poder iniciar sesión con cualquiera de las cuentas; esta es una de las ventajas de una implementación híbrida. Sin embargo, ha habido instancias en las que un administrador no ha podido iniciar sesión con su cuenta local. En general, esto se debe a que la detección automática enfoca el esfuerzo de inicio de sesión en la instalación local de Lync Server en vez de en Office 365.

Afortunadamente, existe una manera sencilla de solucionar este problema. Cuando utilice el cmdlet de **New-CsOnlineSession** para iniciar sesión en Office 365, solo incluya el parámetro OverrideAdminDomain y después el nombre de dominio de Office 365. Por ejemplo, para iniciar sesión en Office 365 con la cuenta administrator@litwareinc.net, incluya el parámetro OverrideAdminDomain y después el nombre de dominio litwareinc.onmicrosoft.com:

    $session = New-CsOnlineSession -Credential $credential -OverrideAdminDomain "litwareinc.onmicrosoft.com"

Este comando conducirá el intento de inicio de sesión explicitamente a los servidores de Office 365 y al dominio litwareinc.onmicrosoft.com.

