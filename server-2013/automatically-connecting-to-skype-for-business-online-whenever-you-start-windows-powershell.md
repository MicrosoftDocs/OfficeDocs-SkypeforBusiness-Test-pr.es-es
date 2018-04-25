---
title: Conectar automáticamente con Lync Online siempre que se inicie Windows PowerShell
TOCTitle: Conectar automáticamente con Lync Online siempre que se inicie Windows PowerShell
ms:assetid: 68f76c36-5dd6-48ea-b19a-d65593199e4c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362799(v=OCS.15)
ms:contentKeyID: 56271311
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Conectar automáticamente con Lync Online siempre que se inicie Windows PowerShell

 

_**Última modificación del tema:** 2015-06-22_

Si no recuerda todos los comandos necesarios para conectarse a Skype Empresarial Online, puede configurar cosas para solo tener que hacer doble clic en un archivo de acceso directo y escribir su contraseña de Skype Empresarial Online: solo con esto se conectará a Skype Empresarial Online.

Para hacerlo, abra Bloc de notas (o cualquier otro editor de texto) y pegue los comandos siguientes sustituyendo el nombre de su cuenta de Skype Empresarial Online por kenmyer@litwareinc.com:

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $session = New-CsOnlineSession -Credential $credential 
    Import-PSSession $session

Guarde el archivo con una extensión de archivo .PS1 (por ejemplo, C:\\Scripts\\LyncOnline.ps1).

Después de guardar el archivo, siga estos pasos para crear un acceso directo de escritorio que inicie Windows PowerShell y ejecute el script al iniciar:

1.  Haga clic con el botón secundario en el escritorio y haga clic en **Nuevo** y en **Acceso directo**.

2.  En el asistente **Crear acceso directo**, escriba lo siguiente en el cuadro **Escriba la ubicación del elemento** y haga clic en **Siguiente** (acuérdese de usar la ruta de acceso del archivo de script que acaba de crear):
    
        powershell.exe -noexit C:\Scripts\LyncOnline.ps1

3.  En el cuadro **Escriba un nombre para este acceso directo**, escriba un nombre para el acceso directo (por ejemplo, **Skype Empresarial Online**) y haga clic en **Finalizar**.

4.  La próxima vez que use Windows PowerShell para administrar Skype Empresarial Online, solo tendrá que hacer doble clic en el nuevo acceso directo y escribir la contraseña. El script se encargará de establecer la conexión y configurar la nueva sesión remota.

Normalmente, esta nueva sesión no se almacenará en la variable $session, sino que se le asignará el id. de sesión 1. Esto no afectará a su sesión de ninguna forma o, al menos, no lo hará hasta que se acerque el momento de cerrar la sesión. Para hacerlo, tendrá que hacer referencia al id. de la sesión al llamar al cmdlet **Remove-PSSession**:

    Remove-PSSession 1

Puede consultar el id. asignado a su sesión de Skype Empresarial Online ejecutando este comando desde el símbolo del sistema de Windows PowerShell:

    Get-PSSession

## Vea también

#### Conceptos

[Configurar el equipo para la administración de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

