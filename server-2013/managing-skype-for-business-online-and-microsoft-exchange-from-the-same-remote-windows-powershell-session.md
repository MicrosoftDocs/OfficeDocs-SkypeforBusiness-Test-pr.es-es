---
title: Administrar Lync Online y Microsoft Exchange desde la misma sesión remota de Windows PowerShell
TOCTitle: Administrar Lync Online y Microsoft Exchange desde la misma sesión remota de Windows PowerShell
ms:assetid: 4eb4b5f0-f407-46bd-a2ac-a7ccbc387d51
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362787(v=OCS.15)
ms:contentKeyID: 56271287
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Administrar Lync Online y Microsoft Exchange desde la misma sesión remota de Windows PowerShell

 

_**Última modificación del tema:** 2015-06-22_

Al suscribirse a Office 365, podrá acceder no solo a Skype Empresarial Online, sino también a Exchange Online. Puede usar una sesión remota de Windows PowerShell para administrar Skype Empresarial Online. También puede usar una sesión remota de Windows PowerShell para administrar Exchange. Sin embargo, Skype Empresarial Online y Exchange Online no comparten el mismo URI ni usan el mismo método de conexión. Esto significa que tiene que usar sesiones diferentes para administrar Skype Empresarial Online y Exchange. ¿O acaso existe alguna forma de administrar ambos productos usando una sola sesión remota de Windows PowerShell?

Resulta que sí: no solo podemos administrar ambos productos desde la misma instancia de Windows PowerShell, sino que configurar esta sesión de administración doble es tremendamente fácil. Para empezar, inicie Windows PowerShell y conéctese a Skype Empresarial Online como siempre: cree un objeto de credenciales y luego cree una sesión nueva que se conecte a Skype Empresarial Online:

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $lyncSession = New-CsOnlineSession -Credential $credential

Después, siga un proceso parecido para conectarse a Exchange Online. Recuerde que no es necesario crear un nuevo objeto de credenciales. Puede seguir usando el mismo objeto ($credential) que usó al iniciar sesión en Skype Empresarial Online:

    $exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection

Debe utilizar siempre el URI https://outlook.office365.com/powershell-liveid/ para conectarse a Exchange Online. Hágalo independientemente del URI de su Office 365. Después de autenticarse, siempre se le redirigirá automáticamente al URI correspondiente. Por ello resulta especialmente importante que incluya el parámetro AllowRedirection. Si lo omitiera, se le autenticaría, pero la redirección fallaría y no se conectaría a Exchange Online:

    New-PSSession : [ps.outlook.com] The WinRM service cannot process the request because the request needs to be sent to a different machine. Use the redirect information to send the request to a new machine.  Redirect location reported: https://pod51043psh.outlook.com/powershell-liveid?PSVersion=3.0 . To automatically connect to the redirected URI, verify  MaximumConnectionRedirectionCount" property of session preference variable "PSSessionOption" and use "AllowRedirection" parameter on the cmdlet.

Llegados a este punto, en su PC debería haber dos sesiones remotas distintas. Para comprobarlo, escriba el comando siguiente en el símbolo del sistema de Windows PowerShell:

    Get-PSSession

En la pantalla, debería ver una información parecida a esta:

    Id Name      ComputerName  State   ConfigurationName     Availability
    -- ----      ------------  -----   -----------------     ------------
     1 Session1  pod510w43...  Opened  Microsoft.PowerShell     Available
     2 Session2  up02921vd...  Opened  Microsoft.Exchange       Available

Ahora tiene un par de sesiones remotas que se pueden importar a la sesión local de Windows PowerShell. Para hacerlo, ejecute estos dos comandos:

    Import-PSSession $lyncSession
    Import-PSSession $exchangeSession

Ahora tendrá los cmdlets de Skype Empresarial Online y de Exchange Online disponibles para su uso. Para comprobarlo, ejecute el comando siguiente y asegúrese de recibir información de usuario:

    Get-CsOnlineUser -ResultSize 1

Luego ejecute el siguiente comando de Exchange y compruebe si recibe información de buzón de correo:

    Get-Mailbox -ResultSize 1

Cuando quiera terminar la sesión de administración, asegúrese de cerrar las dos sesiones remotas:

    Remove-PSSession $lyncSession
    Remove-PSSession $exchangeSession

## Vea también

#### Conceptos

[Configurar el equipo para la administración de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

