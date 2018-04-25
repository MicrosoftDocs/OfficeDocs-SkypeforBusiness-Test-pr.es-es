---
title: Combinar cmdlets de Lync Online y Windows PowerShell
TOCTitle: Combinar cmdlets de Lync Online y Windows PowerShell
ms:assetid: 8bb8800a-f966-4570-8c8b-db87a91ad783
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn362816(v=OCS.15)
ms:contentKeyID: 56271324
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Combinar cmdlets de Lync Online y Windows PowerShell

 

_**Última modificación del tema:** 2015-06-22_

Cuando se conecta a Skype Empresarial Online con Windows PowerShell, tiene disponibles para usar aproximadamente 40 cmdlets de Skype Empresarial Online. Pero esta limitación de 40 cmdlets no se aplica al administrar Skype Empresarial Online. Además de los cmdlets de Skype Empresarial Online, también puede usar cualquier otro cmdlet de Windows PowerShell que tenga instalado en el equipo. (Cuando se instala Windows PowerShell 3.0, también se instalan cientos de cmdlets de Windows PowerShell básicos). Los comandos pueden combinarse con cmdlets de Skype Empresarial Online y con cualquier otro cmdlet disponible en el equipo.

Si bien en este artículo no se ofrece un curso completo de Windows PowerShell 3.0, se proporcionan algunos ejemplos para mostrarle las ventajas de combinar cmdlets. En primer lugar, ninguno de los cmdlets de Skype Empresarial Online incluye el comando Print, que tampoco se encuentra en la consola de Windows PowerShell. Entonces, se preguntará cómo puede imprimir la información recuperada por un cmdlet. Una forma de hacerlo es recuperar la información y enviarla al cmdlet **Out-Printer**:

    Get-CsTenant | Out-Printer

Como no se incluye ningún parámetro adicional, toda la información devuelta por el cmdlet **the Out-Printer** se imprimirá en la impresora predeterminada.

De la misma manera, ninguno de los cmdlets de Skype Empresarial Online incluye un parámetro que le permite guardar datos en un archivo. Pero no hay problema, ya que este comando usa el cmdlet **Out-File** para guardar la información devuelta en el archivo de texto C:\\Logs\\Tenants.txt:

    Get-Tenant | Out-File -FilePath "C:\Logs\Tenants.txt"

Y este comando usa el cmdlet **Select-Object** para limitar los datos que se devuelven y muestran en pantalla. En este ejemplo, el cmdlet [Get-CsOnlineUser](get-csonlineuser.md) recupera información de todos los usuarios de Skype Empresarial Online y luego se usa el cmdlet **Select-Object** para limitar los datos que se muestran según el valor Identity del usuario y su directiva de archivado:

    Get-CsOnlineUser | Select-Object Identity, ArchivingPolicy

Dado que tendrá a disposición cientos de cmdlets en el equipo, le puede resultar complicado determinar cuáles son de Skype Empresarial Online y cuáles no. Para devolver una lista de los cmdlets de Skype Empresarial Online (y únicamente los cmdlets de Skype Empresarial Online), primero debe determinar el nombre del módulo de Windows PowerShell temporal que contiene todos los cmdlets de Skype Empresarial Online. Para ello, ejecute este comando desde el símbolo del sistema de Windows PowerShell:

    Get-Module

En pantalla verá información similar a la siguiente:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

El módulo cuyo ModuleType es Script es el que contiene los cmdlets de Skype Empresarial Online. Para devolver una lista de esos cmdlets, ejecute **Get-Command** usando el nombre del módulo Script como nombre de módulo:

    Get-Command -Module tmp_5astd3uh.m5v

Es posible que tenga varios módulos cuyo ModuleType es Script. En ese caso, puede ejecutar el siguiente comando para averiguar qué módulo incluye el cmdlet **Get-CsTenant**:

    Get-Command Get-CsTenant

El módulo devuelto para el cmdlet **Get-CsTenant** será el que contiene todos los cmdlets de Skype Empresarial Online:

    CommandType     Name                                               ModuleName
    -----------     ----                                               ----------
    Function        Get-CsTenant                                       tmp_5astd3uh.m5v

## Vea también

#### Conceptos

[Introducción a Windows PowerShell y Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

